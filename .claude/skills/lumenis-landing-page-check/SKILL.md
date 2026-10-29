---
name: lumenis-landing-page-check
description: Test a finished Lumenis HubSpot landing page and its form before launch - desktop and mobile layout, dark mode, links, images and copy - check the page metadata (title, description, social preview and featured image), then submit a real test through the form and confirm the workflow, Salesforce routing and autoresponder all fire, and clean up the test lead. Report pass, fail or blocked per check. Use for any campaign page with a form (Accelerate, trade show, campaign pages) before it goes live.
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
| P8 | Settings | URL slug is final; page is linked to the HubSpot campaign only |
| P9 | Metadata | Every row in [Metadata checks](#metadata-checks) passes |

## Metadata checks

Pages cloned from a past event keep its metadata. The page can look right while search results, link previews in email, Slack, LinkedIn and texts still show the old city and dates. Read the metadata from the page source, not the HubSpot editor: open the preview URL, view source, or run `curl -sL <url> | grep -iE '<title|<meta (name|property)="(description|og:|twitter:)|rel="canonical"'`.

| # | Check | Pass when |
|---|---|---|
| M1 | Page title | `<title>` names this event, city and year (for example `Accelerate Tampa 2027 \| Lumenis Vision`); no past city, year or show; under about 60 characters |
| M2 | Meta description | Names this event, city and dates from the campaign record; reads as one plain sentence; about 120-155 characters |
| M3 | Social title and description | `og:title`, `og:description`, `twitter:title` and `twitter:description` match M1 and M2 (HubSpot copies them from the page settings, so a stale title shows up in all of them) |
| M4 | Featured image | `og:image` is set and loads. Use the page's own cleared hero or event image, 1200 x 630 px. If the page has none, use the fallback below. Never leave it empty: link previews then show a blank card or a random image from the page |
| M5 | Card type | `twitter:card` is `summary_large_image` when a featured image is set |
| M6 | Canonical URL | `rel="canonical"` and `og:url` point to the final live URL, not a test, clone or past-event slug |
| M7 | Favicon | The Lumenis Hero L favicon loads |
| M8 | Preview | Paste the URL into a link preview tool (LinkedIn Post Inspector, or a message to yourself in Slack or Teams) and confirm the card shows the right title, description and image |

**Fallback featured image:** [the white Hero L on Lumenis Black, 1200 x 630](../../../assets/design-system/lumenis-corporate/assets/logo/lumenis-hero-l-white-on-black-share-1200x630.png). Upload it once to the HubSpot File Manager and set it as the page's featured image in Settings. It is a brand-only image, so it is cleared for any Lumenis page, but an event image is better when one is cleared.

The test has two parts, run at different times:

- **Pre-launch check** (before launch; D10 for an Accelerate): the page checks above, plus steps 1-2 below on the page preview, plus the workflow checked with HubSpot's own test tools while it is still OFF. The page may be published only when every pre-launch row passes.
- **Live test** (launch day, L0 for an Accelerate): steps 1-6 on the published page, after a person has turned the workflow ON, and only when a person has authorized the test. Nothing is distributed (no flyer, email or social post) until the live test passes.

## Form and workflow test

1. Submit the form with the test email and ZIP `00000`.
2. **Success message** appears and says the right thing for the page (for an Accelerate interest form: thanks, a Lumenis sales representative will reach out; never that they're registered).
3. **Workflow:** the test contact enrolls; Latest Lead Info is set first with this show's text.
4. **Salesforce:** the lead appears in the right campaign with the expected status, assigned by the test ZIP, not to a rep.
5. **Autoresponder:** arrives at the test inbox; passes [lumenis-email-check](../lumenis-email-check/SKILL.md).
6. **Clean up:** remove the test contact from the campaign and delete or mark it as test in HubSpot and Salesforce, per marketing operations' rule.

## Report

Pass, fail with the fix, or blocked with what's missing, per row, labelled pre-launch or live. Save it in the project folder and link it from the Smartsheet row. Pre-launch rows must all pass before the page is published; live rows must all pass before anything is distributed. If a live row fails, a person turns the workflow OFF or unpublishes the page until it's fixed.
