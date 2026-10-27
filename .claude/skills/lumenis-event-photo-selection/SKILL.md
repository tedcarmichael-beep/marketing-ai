---
name: lumenis-event-photo-selection
description: Pick the best photos from an event shoot in Dropbox using the shared selection rubric, copy them into the Dropbox Selected Images library, then run them through the image catalog intake (metadata, WebP, HubSpot upload, catalog sync) in one pass. Use when someone asks to review, choose or add photos from an Accelerate event, trade show or other Lumenis event.
---
# Select event photos and add them to the image catalog

Owner: Ted Carmichael (marketing).
Status: draft procedure, tested 2026-10-27 on two event shoots (a trade show with a dinner, and an Accelerate summit); maintainer and subject-owner review required.

One run takes an event shoot from Dropbox to live catalog entries:

1. choose 10–15 photos per event with the [selection rubric](references/selection-rubric.md);
2. copy them into the Dropbox `/Selected Images` library;
3. add them to the shared image catalog through the [image library workflow](../../../assets/image-library/README.md): metadata, WebP derivatives, HubSpot upload, catalog sync.

The rubric decides *which* photos; the image library workflow decides *how* they enter the catalog. Do not copy its rules here.

## Inputs and prerequisites

Stop and ask if any essential input is missing.

| Input | Notes |
|---|---|
| Event shoot folder(s) in Dropbox | Usually `.../<event>/Media Captured at Show/`. An event can have several subfolders (booth, dinner); review each. |
| Business unit and collection | `businessUnit` (Vision, Aesthetics, Corporate) routes the HubSpot folder. Collection is usually `accelerate-events` or `trade-shows`; see `assets/image-library/scripts/helpers/schema.mjs`. |
| Brand scope | `allowedBrands`. Use `unclassified` unless the person running the task has decided it. |
| Authorization for the full run | Before any write, state the plan once: the Dropbox copies, the HubSpot portal (278427) and the business-unit folder. One confirmation covers the run. Without it, stop after step 3 and report the picks. |

Tools: a Dropbox connector that can list, download and copy (for example the Dropbox MCP `list_folder`, `download_link`, `copy`, `check_job_status`); Node.js 22 with the image library installed (`npm ci` in `assets/image-library`); the HubSpot CLI already authenticated as yourself. If HubSpot access is unavailable, finish through step 6 and report that upload is pending. Never request, store or type credentials.

## Procedure

1. **List the shoot.** List each event folder recursively and record file id, name and path for every image. Check `/Selected Images` for photos from this event that are already there, so you don't duplicate or overwrite them.
2. **Review every photo.** Download through single-use links into a temporary working folder outside the repository, resize to about 700 px, and build numbered contact sheets (16 per sheet works well). Look at every sheet. Never judge a photo from its filename.
3. **Pick with the rubric.** Shortlist, dedupe bursts with the tie-breakers, then trim to about 3–5% of the shoot (10–15 picks for 250–350 photos). Check the people / no-people balance and the hard rejects. Record a one-line reason per pick.
4. **Copy to Dropbox.** Copy each pick by file id to `/Selected Images/<original filename>` with `autorename: false`. Only copy: never move, rename or delete originals. If `/Selected Images` is mirrored elsewhere (for example a design-system media staging folder), don't write to the mirror. Poll `check_job_status` until complete, and read back the result.
5. **Stage for the catalog.** Download each pick's full-resolution original into `assets/image-library/1-raw/` (ignored by Git).
6. **Describe and process.** For each pick, run `npm run generate-metadata` with a unique ID such as `lumenis-accelerate-stage-wall-001`, then look at the photo and fill every field following the image library README. Write `usageRestrictions` from what you actually see: identifiable people (releases), patients or treatment (consent), competitor or partner branding, on-screen data. Put the drafts in `2-metadata/batch.json`, run `npm run process-image -- --batch batch.json`, then `npm run validate-catalog -- --metadata-only --allow-pending`. Inspect the generated WebP sizes.
7. **Upload and sync.** Using the authorization from the inputs step, confirm the account and folder against the live account (see the image library README), then run `npm run upload`, `npm run sync-catalog` and `npm run validate-catalog -- --metadata-only`. Inspect the catalog diff, especially removed URLs.
8. **Propose the catalog change.** Commit `catalog.json` and the regenerated `catalog.md` on a branch and open a pull request, following [contributing](../../../CONTRIBUTING.md). Image bytes, the working folder and rights evidence stay outside the repository.

## Result

Report, per event: the picks with Dropbox paths and one-line reasons, the people / no-people count, the new catalog IDs with their HubSpot URLs, and anything pending (upload not run, rights unverified, `unclassified` brand scope). A photo in `/Selected Images` or HubSpot is not rights clearance; `usageRestrictions` lists what a person must check before publishing.

## When something is missing

- **No shoot folder or empty folder:** stop and ask for the path.
- **No authorization for writes:** do steps 1–3, report the picks, and stop.
- **Filename already in `/Selected Images`:** skip it and report; don't overwrite or autorename.
- **Too few strong photos:** pick fewer. Don't fill the target with weak frames.
- **HubSpot auth or scope failure:** diagnose it as the image library README describes. Don't switch tools or reinitialize the CLI. Leave the derivatives pending and report.

## Feedback loop

When the person reviewing the picks swaps photos, ask why, and propose the reason as a rubric change in a pull request. Taste corrections belong in the rubric, not in a chat history.
