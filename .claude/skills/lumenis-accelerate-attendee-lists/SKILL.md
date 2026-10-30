---
name: lumenis-accelerate-attendee-lists
description: Build every Accelerate attendee list from Smartsheet - the badge file for the badge printer, the OneTap check-in upload (after archiving and clearing the previous show), the Know Before You Go segment for HubSpot, and the attended list after the show for HubSpot and Salesforce. Use whenever an Accelerate needs a list of who is coming or who came. Smartsheet is the source; HubSpot is not.
---

# Accelerate attendee lists

Owner: EJ (marketing operations), with Kaelyn for badges and OneTap.
Status: draft procedure, written 2026-10-29 from the Vision Accelerate planning session; not yet run. Review required. Name and duplicate rules added 2026-10-30 from a completed badge build; owner to confirm.

Four lists come from the same source at different times. Building them one way keeps the counts consistent and stops anyone pulling a list from HubSpot, where form fills are not registrations.

## Source

The event folder's sheets in Smartsheet: **VIS Rep Approval**, **AES Rep Approval**, the **Flight** registration sheet and the **Non-Flight / Local** registration sheet. Read all four, then:

1. **Merge** on the person. Someone on an approval sheet and a registration sheet is one attendee.
2. **Email is not a unique ID.** A practice often routes several people through one inbox, so two names on one address are two people, not a duplicate. Match on full first and last name plus practice, using email only as supporting evidence. Keep distinct first names separate even when surname and practice match. A nickname, changed surname or ambiguous match requires a confirmed identity mapping from the attendee or owner before merging; until then keep source records separate and flag the possible duplicate.
3. **Keep** only rows that are approved and registered for this show (use each sheet's approval and status columns as the event's setup defines them; ask when a column's meaning is unclear).
4. **Division** comes from the sheet (VIS or AES), or the Division column on shared sheets.
5. **Flag, don't fix** whatever the rules below do not settle: rows without an email, duplicates that still conflict, names in all caps. Report them to the owner.

Use the connector's full row read (paginate). A column-filtered summary can omit rows.

Also when reading the sheets:

- An approval row can hold two attendees. Attendee #2 is a person and counts.
- Exclude placeholder and test rows, and the approval sheets' summary rows, where the rep-name cell holds a metric label rather than a person.
- City and state exist only on the registration sheets, so approval-only attendees have none. Leave those badge fields blank rather than guessing.

### Name normalization

These rules apply only to badge display fields after identity matching. Preserve original names and source row IDs separately; do not propagate badge edits to travel, OneTap, HubSpot or Salesforce identity fields. Use each destination's confirmed identity requirements; unresolved shared-email CRM mappings block that import, not badge drafting. Never infer a preferred name or relationship. Apply in order:

1. **Nickname:** use an explicitly recorded or attendee/owner-confirmed preferred badge name. A familiar-looking nickname alone is not identity evidence.
2. **Middle name used as a first name:** use it only when confirmed as the attendee's preferred badge name; otherwise flag the difference and retain the registration name in the draft.
3. **Spelling variants:** once identity is confirmed, use the registration spelling unless a preferred spelling is explicitly confirmed. Uncertain identity stays flagged.
4. **Two surnames on file:** neither a substring nor another attendee's surname proves truncation, marriage or professional use. Retain both source values, flag the discrepancy and obtain attendee/owner confirmation before merging identities or changing the badge surname. A registration name may remain as a clearly flagged draft.
5. **Middle names:** omit only when they are not part of the confirmed preferred badge name; never drop a middle name used as the first name.
6. **A missing surname does not block the list.** Leave it blank and report it.

### Duplicate resolution

1. A shared email is not a duplicate.
2. The same person entered twice on one sheet collapses to one row. Check whether one of the two rows has values shifted into the wrong columns before choosing which to keep.
3. The same surname at one practice does not establish a duplicate or a relationship. Different people remain separate; ambiguous full-name matches need owner confirmation.
4. When duplicate rows disagree on city or practice name, confirm the practice's location from a public source instead of taking the first row. A city field sometimes holds the nearest airport rather than the practice's town.
5. A confirmed person already counted who later appears on a second sheet does not raise the headcount. Compare confirmed identity mappings and source row IDs, not email or row counts alone. Report unresolved possible duplicates separately; do not call their count reconciled.

## Lists

| Step | When | List | Fields | Goes to |
|---|---|---|---|---|
| E12 | T-11 | Badge file | First name, last name, account (practice), city, state, division, email | Badge printing vendor (they ask about ten days out). Two badge styles, Vision and Aesthetics. Tell them email is contact data, may be shared and must not print; preserve a distinct attendee key for each person |
| D11 | T-4, Monday morning | Know Before You Go | Email, first name, last name, division | HubSpot static segment attached to Em2; set **Registered** in the Salesforce campaign |
| L1 | T-1 | OneTap upload | As OneTap's import template requires | OneTap, after the archive step below |
| P1 | T+3, Monday after | Attended | From OneTap check-ins | HubSpot segment for Em3 (sends Tuesday); set **Attended** in the Salesforce campaign |

### OneTap archive before upload (L1)

OneTap holds one show at a time. Before uploading:

1. **Export** all of the previous show's OneTap data and save it in that show's OneDrive attendee records folder. Open the export and check the row count.
2. Only then **delete** the previous show's data from OneTap.
3. **Upload** this show's list and check the count matches the Smartsheet list.

Never delete before the export is saved and checked.

## Output

Counts per list and division, the flagged rows, and where each file went. Save files in the project folder, put counts in Key Info. Imports into HubSpot or Salesforce and vendor hand-offs are done by the owner after review.

## Boundaries

- Never build an attendee list from HubSpot contacts or form submissions.
- Attendee files contain personal data: keep them in OneDrive and the target system only, never in this repository, chat history beyond the task, or public links.

## Fictional walkthroughs

- Alex Example and Jordan Example at one practice share an inbox. Different first names keep them as two attendees and two badge rows.
- One sheet says Elizabeth Sample and another says Liz Sample. Flag a possible match and retain both records until the owner confirms identity and the preferred badge name.
- Two surname variants overlap or match a coworker's surname. Neither proves identity; preserve both values and request confirmation.
- A confirmed attendee prefers a middle name as their first name. Use that name on the badge and retain the original registration fields for travel and system matching.
