---
name: lumenis-event-photo-selection
description: Pick the best photos from a Lumenis event shoot in Dropbox using the shared selection rubric, copy them into the team's Selected Images folder, then hand the cleared picks to the image library workflow for catalog intake and HubSpot upload in the same run. Use when someone asks to review, choose or add photos from an Accelerate event or a trade show.
---
# Select event photos and add them to the image catalog

Owner: marketing (event photography).
Status: draft procedure. Steps 1–4 were executed 2026-10-27 on two Vision event shoots (a trade show with a dinner, and an Accelerate summit). Step 5 was executed locally through processing and validation on one image; the HubSpot upload has not yet been run from this skill. Subject-owner review required.

One run takes an event shoot from Dropbox to the image catalog. You pick photos with the [selection rubric](references/selection-rubric.md), get one approval of the actual picks, copy them to Selected Images, then add the cleared picks through the [image library workflow](../../../assets/image-library/README.md). This skill decides *which* photos and *when*. The image library README remains the only procedure for metadata, processing, upload and sync.

## Inputs

Stop and ask if any of these is missing.

- **The event shoot folder(s) in Dropbox**, usually `.../<event>/Media Captured at Show/`. An event can have several sub-shoots (booth, dinner); review each one.
- **The team's Selected Images folder.** It is usually `/Selected Images` at the team Dropbox root and flat (no subfolders). If you can't find it, ask; don't create one.
- **Business unit and brand scope** for the image library stage. Ask if they aren't given.
- **A Dropbox connector** that can list, download and copy (for example the Dropbox MCP `list_folder`, `download_link`, `copy`, `check_job_status`). The image library stage has its own prerequisites, listed in its README.

## Procedure

1. **List the shoot.** List each event folder recursively and record the file id, name and path of every image. Note which photos from this event are already in Selected Images.
2. **Review every photo.** Download through single-use links into a temporary folder outside the repository, resize to about 700 px, and build numbered contact sheets (16 per sheet works well). Look at every sheet. Never judge a photo from its filename.
3. **Pick with the rubric.** Shortlist, dedupe bursts with the tie-breakers, then trim to the rubric's target. Record a one-line reason per pick. Mark any pick whose main subjects are identifiable attendees (not staff, speakers or KOLs) as **catalog pending decision**; see the rubric's open questions.
4. **Get one approval, then copy.** Show the picks (a contact sheet plus the reasons) and ask once for approval to do all three of these:
   - copy exactly these files to the named Selected Images folder;
   - upload exactly the cleared picks (not those marked pending) to portal 278427 and the named business-unit folder;
   - open a catalog pull request.

   Apply swaps the person asks for before anything is written. Without approval, stop here and report the picks.

   After approval, copy each pick by file id to `<Selected Images>/<original filename>` with `autorename: false`. Only copy: never move, rename or delete originals. If a filename already exists, skip it and report it. Poll `check_job_status` until the copy completes, and read back the result.
5. **Hand off to the image library.** Put each cleared pick's full-resolution original in `assets/image-library/1-raw/`. Then follow the [image library workflow](../../../assets/image-library/README.md) from "Add and describe an image" through upload, sync and validation, with the values below.

   Before upload, list the pending catalog entries. If any ID isn't from this run, stop and report it, because upload sends every pending entry. If the approval didn't cover a step (upload, or the pull request), stop before it.

   Event-specific values for that workflow:

   | Field | Value for event photos |
   |---|---|
   | `collection` | `accelerate-events` or `trade-shows` |
   | `id` | `lumenis-<event-type>-<subject>-NNN`, for example `lumenis-accelerate-stage-wall-001` |
   | `allowedBrands` | `unclassified` unless the brand scope was given |
   | `usageRestrictions` | What you see: identifiable people (releases), patients or treatment (consent), partner or competitor branding, on-screen data |

## Result

Report the following for each event:
- the picks, with their Selected Images paths and one-line reasons;
- the count of photos with and without people;
- any picks marked catalog pending decision;
- the new catalog IDs with their HubSpot URLs;
- anything pending: upload not run, rights unverified, `unclassified` brand scope.

Being in Selected Images or HubSpot does not mean rights are cleared.

## When something is missing

- **No shoot folder, or an empty folder:** stop and ask for the path.
- **No approval of the picks:** report the picks and stop after step 3.
- **The image library stage can't run** (no HubSpot access, a failed check): the Dropbox copies stand. Report which catalog steps are pending and follow the image library README's failure guidance.
- **Too few strong photos:** pick fewer. Don't fill the target with weak frames.

## Feedback loop

When the reviewer swaps picks in step 4, ask why, and propose the reason as a rubric change in a pull request. Taste corrections belong in the rubric, not in a chat history.
