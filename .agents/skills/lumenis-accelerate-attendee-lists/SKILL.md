---
name: lumenis-accelerate-attendee-lists
description: Build every Accelerate attendee list from Smartsheet - the badge file for the badge printer, the OneTap check-in upload (after archiving and clearing the previous show), the Know Before You Go segment for HubSpot, and the attended list after the show for HubSpot and Salesforce. Use whenever an Accelerate needs a list of who is coming or who came. Smartsheet is the source; HubSpot is not.
---

# Accelerate attendee lists

Owner: EJ (marketing operations), with Kaelyn for badges and OneTap.
Status: draft procedure, written 2026-10-29 from the Vision Accelerate planning session; not yet run. Review required.

Four lists come from the same source at different times. Building them one way keeps the counts consistent and stops anyone pulling a list from HubSpot, where form fills are not registrations.

## Source

The event folder's sheets in Smartsheet: **VIS Rep Approval**, **AES Rep Approval**, the **Flight** registration sheet and the **Non-Flight / Local** registration sheet. Read all four, then:

1. **Merge** on email (the unique ID). A person on an approval sheet and a registration sheet is one attendee.
2. **Keep** only rows that are approved and registered for this show (use each sheet's approval and status columns as the event's setup defines them; ask when a column's meaning is unclear).
3. **Division** comes from the sheet (VIS or AES), or the Division column on shared sheets.
4. **Flag, don't fix:** rows without an email, duplicates with conflicting details, names in all caps or with obvious typos. Report them to the owner.

Use the connector's full row read (paginate). A column-filtered summary can omit rows.

## Lists

| Step | When | List | Fields | Goes to |
|---|---|---|---|---|
| E12 | T-11 | Badge file | First name, last name, account (practice), city, state, division, email | Badge printing vendor (they ask about ten days out). Two badge styles, Vision and Aesthetics. Tell them email is an ID only and must not print |
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
