---
name: lumenis-accelerate-pipeline-review
description: Turn a recorded Accelerate pipeline review (the RSM-led call where reps walk through each attending account) into short per-account notes on the Rep Approval sheet - deal status, what will close it, and what the rep needs at the show. Use after each pre-show pipeline review call. Writes only the notes column.
---

# Accelerate pipeline review notes

Owner: EJ (marketing operations); the review itself is run by the division's leading RSM.
Status: draft procedure, written 2026-10-29 from the Vision Accelerate planning session; not yet run. Review required.

About two weeks and one week before the show, the leading RSM for each division holds a pipeline review with every rep who has an account attending. Each rep says where the deal stands and what it needs to close: a conversation with a KOL, clinical time, a particular session, something from marketing. The call is recorded. Sales then uses the sheet on show day to assign deals to reps on the floor, so the notes have to be on the right rows and easy to scan.

## Inputs

- The call transcript (Teams or the meeting recorder), saved in the project folder.
- The division's Rep Approval sheet, with [pipeline sync](../lumenis-accelerate-pipeline-sync/SKILL.md) already run so each row has its opportunity, amount and stage.
- The notes column the event setup uses for review notes. If the sheet has none, stop and ask the owner to add one; don't invent a column.

## Procedure

1. **Match** each account discussed to its row: practice name first, then rep plus city. When two rows could match, or none does, list it as unmatched; don't guess.
2. **Write one note per row,** at most three short lines:
   - **Status:** the rep's words on where the deal is (for example "quote out, waiting on partner sign-off").
   - **To close:** what the rep said it needs (KOL talk, clinical demo, financing, a session).
   - **At the show:** the action and who owns it.
   Date-stamp each note (`Review 1, <date>:`). Review 2 adds a new note; it doesn't overwrite review 1.
3. **Present the change set** (row, note) and the unmatched accounts. Write when the request authorizes it; otherwise wait for approval.
4. **Write** one batch to the notes column only, then read the column back.

## Boundaries

- Notes reflect what was said. Don't add opinions, forecasts or values Salesforce doesn't hold.
- Never change Amount, Stage or Expected Value here; that's pipeline sync.
- Transcripts and notes stay in the project folder and Smartsheet, never in this repository.
