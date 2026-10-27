---
name: lumenis-photo-selection
description: Review photos in one or more supplied Dropbox, shared or local folders, propose reusable library selections, and add approved picks to the HubSpot image repository through the existing image-library workflow. Use for event shoots, products, headshots, facilities or other photo collections; no future campaign or use is required.
---
# Select photos for the image library

Owner: marketing (photo library); proposed subject reviewer: Ted Carmichael.
Status: draft procedure. The original event selection and Dropbox copies were executed 2026-10-27 on two Vision shoots. Local image-library processing was checked on one image; upload from this skill and non-event selection remain untested. Generalized by Nicholas's instruction; subject-owner review required for additional selection guidance.

Build a reusable HubSpot image repository, not an asset set for a specific campaign. The catalog's descriptions, tags and hosted URLs let AI choose suitable images later. No future placement, campaign or intended use is required to select photos. The [image library workflow](../../../assets/image-library/README.md) remains the canonical procedure for metadata, processing, upload, sync and catalog contributions.

## Inputs

- **One or more source folders**, resolved from the request or established context. Ask for the folder(s) if unclear. Dropbox folders need a connector that can list and download, plus copy when a Selected Images copy is requested. Local or synced shared folders need file access. Stop the affected step if access is unavailable.
- **Selected Images destination**, when the team wants an additional Dropbox copy. Use the supplied or established team folder; ask if that copy is requested but its destination is unclear. Don't create a destination by guessing. A Selected Images copy is not required for catalog intake from another source.
- **Business unit**, resolved before HubSpot intake for folder routing. Ask only if it cannot be established. Missing routing blocks upload, not independent photo review. Brand permissions follow existing evidence; unknown scope remains `unclassified`.

## Procedure

1. **Inventory the folders.** List recursively, including all pages of results. Record stable file IDs or paths, names and source locations outside Git. Check for prior Selected Images copies and catalog entries before adding duplicates.
2. **Review the photos.** Build numbered contact sheets from temporary copies outside Git (about 700 px previews, 16 per sheet works well). Inspect every sheet, then full-resolution shortlisted images for sharpness and details. Never judge from filenames alone.
3. **Propose selections** using [selection guidance](references/selection-guidance.md). Use the [event rubric](references/selection-rubric.md) only for event shoots; its people ratios and category priorities do not govern product, headshot or facility folders. Record a reason for each pick. Identifiable event-attendee picks remain **catalog pending decision**, as the event rubric specifies.
4. **Show the actual picks before writes.** Provide a contact sheet and reasons, including pending items. Follow existing task authorization; if it doesn't cover the final picks and writes, obtain one approval naming the source files, any Selected Images copies, portal 278427 and its business-unit folder, and the catalog contribution. Apply requested swaps before writing. Never upload picks still marked pending.
5. **Copy when requested.** Copy approved picks to the named Selected Images folder using original filenames and no autorename. Never move, rename, overwrite or delete originals. On a filename collision, compare identity/content: reuse an identical copy; flag a different file and leave it untouched. A collision doesn't substitute that different file for the approved original in catalog intake. Read copied results back; wait for asynchronous copy jobs when applicable.
6. **Add approved picks to the image library.** Put working copies of full-resolution originals in `assets/image-library/1-raw/`, then follow the linked image-library workflow from metadata through validation, authorized upload and sync. Use a suitable existing schema collection; never force non-event photos into an event collection. If none fits, report the metadata decision before intake.

   Metadata describes what is actually visible: subject, action, background, products, people, orientation, tags, alt text and restrictions. Record potentially suitable audiences and placements as descriptive suggestions, not a required future use or proof of approval. Use `unclassified` for unknown brand permissions. Do not infer releases or consent from someone's role, source availability or approval of the selection.

   Choose unique schema-compliant IDs ending in three digits. Keep an external mapping from approved source file to catalog ID. Before upload, compare every pending entry with that mapping: upload only approved, non-pending picks from this run. Stop if unrelated pending entries exist, because the uploader sends all pending derivatives. Keep confidential source and rights evidence outside the public catalog. Follow the existing repository PR process for catalog metadata and URLs; originals stay outside Git.

## Result and missing inputs

Report picks with source identities, reasons, any Selected Images paths, catalog IDs and verified HubSpot URLs. Separate finished work from pending decisions, missing access and rights uncertainty. Being in Selected Images or HubSpot does not establish reuse clearance.

- No source folder or unreadable/empty folders: report the gap and ask for the affected folder/access.
- No approval for a required write: report selections and stop before that write.
- No HubSpot capability or failed validation: preserve finished copies and report remaining intake/upload steps.
- Too few strong photos: pick fewer; never fill quotas with weak frames.

## Feedback loop

Keep event taste refinements in the event rubric. Propose general selection improvements separately, with their scope and evidence, through contribution review. Do not turn one shoot's preferences into rules for every photo collection.
