---
name: lumenis-accelerate-attendee-report
description: Profile the practices registered for an Accelerate - devices they already own and products they're interested in, per division - for the sales VPs, marketing leadership and the session line-up, and build the current-owners list the service team uses to prepare. Use about two weeks before an Accelerate. Reads Smartsheet and Salesforce; writes a report, not records.
---

# Accelerate attendee report

Owner: EJ (marketing operations).
Status: draft procedure, written 2026-10-29 from the Vision Accelerate planning session; not yet run. Review required.

Two weeks out, the team decides which sessions to run (for example a double DMST track versus the medical model session) from who is coming. Service also wants to know which current owners are coming so it can prepare. Both come from the same read.

## Inputs

- The VIS and AES Rep Approval sheets for the show (registered prospects and their Salesforce opportunity links, product of interest).
- Salesforce, read-only, through the logged-in browser session or connector the team uses for [pipeline sync](../lumenis-accelerate-pipeline-sync/SKILL.md). Never request credentials.

## Procedure

1. **Read** every registered row on both sheets (paginate). Skip rows marked Duplicate by pipeline sync.
2. **Owned devices:** for each account, read the installed Lumenis products (asset or install records on the Salesforce account). If the read fails, mark "unknown", don't guess.
3. **Interest:** the sheet's Product of Interest plus the opportunity's product.

### S3 Attendee profile (T-14)

Per division, a one-page summary:

- Registered practices and people.
- Counts by device already owned and by product of interest, and how many are new to IPL or dry eye (no Lumenis IPL owned).
- Three lines on what this means for the session line-up. Recommend; the content owner decides (C9).

Send to the division's sales VP, marketing leadership and the marketing team. Save in the project folder.

### S2 Current owners list (T-16)

An Excel file of registered accounts that already own a device: practice, city, state, rep, devices owned. Draft the email to the service lead with the file attached.

## Boundaries

- Read-only in Salesforce and Smartsheet.
- Practice names and pipeline figures stay in the work systems and the project folder, never in this repository.
