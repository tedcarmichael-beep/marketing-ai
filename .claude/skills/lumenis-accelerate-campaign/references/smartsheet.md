---
title: Smartsheet event backend procedure
summary: Existing copy/setup lessons; connector deployment is a later rollout stage.
status: historical procedure; current capability and template inspection required
owner: event manager and marketing operations
reviewed: 2026-10-27
---
# Event backend

This preserves existing operational knowledge, not a claim that the team MCP is configured. Confirm available connector operations and permission scope at runtime. The source connector lacked form/automation tools; use the current web UI for unsupported actions rather than assume that limitation is permanent.

## Shape

One event folder (`Qn City Accelerate`) in the approved workspace, with four sheets: AES Rep Approval, VIS Rep Approval, City Flight Registration (AES+VIS), City Non-Flight Registration (AES+VIS). Six forms: one per approval sheet, two division forms on each registration sheet. Source branding was orange/peach for Aesthetics and blue for Vision.

## Copy and inspect

1. Inspect the approved current template, its sharing and automations. Do not blindly select the newest file or named historical city.
2. Browse → workspace → template folder → Save as New. Name the destination and confirm it. Include needed forms/formatting. Understand the option to include automated workflow recipients/permissions: unchecked can drop them; checked can propagate stale recipients or live alerts. Keep copied notifications disabled or otherwise contained until reviewed; do not send to old recipients during setup.
3. Verify all four destination sheets and newly assigned IDs before modifying. The folder resorts after rename; refresh the list rather than reuse row positions.
4. If old rows copied, remove them only from the verified new copy under the authorized cleanup scope. Confirm total rows and all IDs with pagination; column-filtered summaries can omit blank rows. Preserve intentional spacer/template rows and never clear the source.
5. On both approval sheets update Event Interested in Attending to the new event. Fetch fresh column IDs; copied IDs differ.
   Confirm the RSM Name picklist lists the current RSMs for that division (check the org chart, not the old sheet). On the AES sheet only, confirm the RSM approval column exists (see the gate below).
6. For all six forms update title, description and confirmation message. Save and reopen; the sidebar sometimes rendered the previous form's content. Check division branding and actual form ID before editing. Do not activate a form until its destination and permissions are ready.
7. On the AES Rep Approval sheet only, set up the [RSM approval gate](#rsm-approval-gate). Then inspect travel and internal notifications: triggers, conditions, recipients, subject, full body and permission constraints. Source travel alert used Send to Travel Agent checked; source internal alert used new rows. Confirm current business recipients, not names copied from old docs.
8. Collect six Share Form links and four sheet links, then produce the Master Links and internal document set. Verify destination, division and access from the intended user's account.

## RSM approval gate

**Aesthetics only.** Applies to the AES Rep Approval sheet from Q4 2026 (requested by the Aesthetics sales lead on 2026-10-27). Do not add it to the VIS Rep Approval sheet: Vision keeps the single rep-entered `RSM Approval` column and its own [flight approval check](../../../../divisions/vision/smartsheet/accelerate-flight-approval-check.md).

**Why.** `RSM Approval` is filled in by the rep on the form. It is the rep saying the RSM agreed, not the RSM agreeing. Flights cost real money, so the RSM confirms each submission on the sheet before marketing sends a traveler to Direct Travel.

**Column.** Next to `RSM Approval`, a picklist column `RSM Approved (RSM to complete)` with options `Yes` and `No`. Put it in the sheet, not on the rep form. Column description: "Completed by the RSM, not the rep. Marketing only sends a flight to Direct Travel when this says Yes."

**Notification.** One workflow per sheet, named `Notify RSM of new rep approval - approve in sheet`:

- Trigger: when rows are **added** only, run right away. Do not use "added or changed": the RSM's own edit would re-send the email.
- One condition branch per current RSM: `RSM Name` equals that name → email that RSM's own address. Recipients by email, not "all shared users".
- Subject: `Action needed: approve a rep registration for Accelerate <City>`.
- Body: a rep submitted the form below; mark Yes or No in the RSM column; marketing will not send anyone to Direct Travel until it says Yes; link to the sheet. Include all row fields (the default) so the RSM sees the submission.
- After creating it, read it back and confirm every branch names the right RSM, city and sheet link.

**Access.** Every RSM in the picklist needs Editor access to the sheet, or they cannot mark the column. Viewer is not enough. Share the sheet with an RSM **before** adding them to the workflow: Smartsheet turns the whole workflow off ("disabled by system") if any recipient lacks access, and it stays off until someone turns it back on. After any change, confirm the workflow still shows as on. A rep naming an RSM who is not in the picklist or not shared gets no email; list those rows for marketing.

**Marketing check.** Before ticking Send to DT on an Aesthetics flight registration, confirm the traveler's approval row has `RSM Approved (RSM to complete)` = `Yes`. If it is blank or `No`, do not send; contact the rep and RSM. A rep-entered `RSM Approval` = `Yes` alone is not enough.

**Rollout.** Tell the division lead when the gate is live on a new event so they can review blanks with their RSMs on their weekly call.

## Known source-template failures

RSM alerts showed Unable to run because recipients could not receive notifications under sharing/domain settings. Adding sharing or approved domains is a real access change, not a cosmetic fix; get the appropriate authority and test intended recipients. A copied travel alert's subject was updated while its body still named the old city. The shared Flight sheet's Division picklist had only Vision; check that both intended divisions can be represented and routed. Copied per-RSM alert workflows (Q4 2026 copies) kept the old city name in the subject and body, named RSMs who had left, and one was left enabled. They also fired on any row change, so any later edit re-sent the email. On a new copy, rewrite or disable every copied RSM alert, and check that no copied alert fires on row changes when the sheet now has columns people edit after submission. Never call the backend ready while a required notification remains broken.

Test a synthetic approved registration through every intended division/path and confirm storage and notification behavior. Avoid changing live operational sheets as part of documentation work. The future source-of-truth schema, MCP authentication and team access remain a separate rollout milestone.
