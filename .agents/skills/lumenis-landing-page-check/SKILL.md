---
name: lumenis-landing-page-check
description: Test a finished Lumenis HubSpot landing page and its form before launch - desktop and mobile layout, dark mode, links, images and copy - then submit a real test through the form and confirm the workflow, Salesforce routing and autoresponder all fire, and clean up the test lead. Report pass, fail or blocked per check. Use for any campaign page with a form (Accelerate, trade show, campaign pages) before it goes live.
---

# Landing page check

Owner: marketing operations (EJ for Vision).
Status: draft procedure, written 2026-10-29 from the Vision Accelerate planning session; not yet run. Review required.

The page counterpart of [lumenis-email-check](../lumenis-email-check/SKILL.md). Pages break in the same places emails do (mobile, dark mode, a stale link) and in one more: a form that looks fine but routes the lead nowhere. This skill checks both.

## Inputs

- The page's preview or staging URL and the form on it.
- The campaign record: event name, city, dates, links, the Salesforce campaign and the expected member status, the autoresponder email.
- A team test email address, and the **test ZIP code `00000`**, which routes test leads to marketing operations instead of a sales rep.

## Page checks

| # | Check | Pass when |
|---|---|---|
| P1 | Desktop | 1440 and 1280 px: nothing overlaps, cut off or misaligned |
| P2 | Mobile | 320, 375 and 414 px: text readable, images scale, no horizontal scroll, form usable, buttons tappable |
| P3 | Dark mode | Phone in dark mode: text stays readable, logos and graphics don't vanish or invert badly |
| P4 | Content | City, dates, venue and KOLs match the campaign record; no text from another show; no placeholder or lorem ipsum |
| P5 | Links | Every link and button opens the right page for this show; none to a past event |
| P6 | Images | Load, have alt text, and are cleared for use |
| P7 | Copy | [Ted's clarity gate](../copy-clarity-gate/SKILL.md) and [claims check](../lumenis-claims-check/SKILL.md) pass |
| P8 | Settings | Page title, meta description and URL slug are final; page is linked to the HubSpot campaign only |

## Form and workflow test

Only after the workflow is cloned and checked, and only when the test is authorized.

1. Submit the form with the test email and ZIP `00000`.
2. **Success message** appears and says the right thing for the page (for an Accelerate interest form: thanks, a Lumenis sales representative will reach out; never that they're registered).
3. **Workflow:** the test contact enrolls; Latest Lead Info is set first with this show's text.
4. **Salesforce:** the lead appears in the right campaign with the expected status, assigned by the test ZIP, not to a rep.
5. **Autoresponder:** arrives at the test inbox; passes [lumenis-email-check](../lumenis-email-check/SKILL.md).
6. **Clean up:** remove the test contact from the campaign and delete or mark it as test in HubSpot and Salesforce, per marketing operations' rule.

If the workflow is still OFF, test with its own test tools where available, and repeat step 1-5 on launch day after a person turns it on.

## Report

Pass, fail with the fix, or blocked with what's missing, per row. Save it in the project folder and link it from the Smartsheet row. The page goes live only when every row passes.
