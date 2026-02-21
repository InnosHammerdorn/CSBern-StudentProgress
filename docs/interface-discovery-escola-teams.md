# Interface discovery memo: Escola (escola.ch) + Teams fallback

## Scope
This memo now focuses on the specific vendor site provided by the user: **https://www.escola.ch/**.

## What was directly observed on escola.ch
From Escola public product pages, the following interfaces/integration mechanisms are explicitly visible:

1. **Microsoft 365 School Data Sync (SDS) integration**
   - Escola advertises an automated synchronization module for students (SuS), teachers (LP), classes and groups to Microsoft 365 SDS.
   - It also states that Microsoft identities/accounts can be created automatically for users.

2. **Data import/export interfaces**
   - Mentioned support for imports from XLS, CSV and other formats.
   - Mentioned exports in multiple formats (including PDF, XLSX, V-Card) and list exports as XLS/PDF.
   - Mentioned BISTA export.

3. **"Schnittstellen / Synchronisationen" module area**
   - Escola publicly frames integrations as "Schnittstellen, Synchronisationen und Exporte" (interfaces, synchronizations, exports).
   - The Schulmanager page presents "Schnittstellen" as a dedicated module group.

4. **Reference to third-party ecosystem replacement/overlap**
   - Escola marketing states it replaces tools like Lehreroffice, Klapp, Moodle, iCampus, CMI Schule, Scolaris, etc.
   - This indicates ecosystem overlap, but does **not** by itself confirm an open API for external custom tools.

## What is NOT confirmed yet from public pages
The public pages reviewed do not clearly confirm (at least in the visible marketing content):
- A publicly documented REST/GraphQL API for custom development.
- Public webhook/event subscription endpoints.
- Public OAuth developer portal and app registration flow for third-party apps.
- Parent messaging API endpoints that can be called by external tools.

## Practical conclusion for your planning
For your teacher→parent progress tool, the currently verified integration surfaces are:
- **Batch/sync style interfaces** (imports/exports + Microsoft SDS synchronization) rather than clearly documented open developer APIs.

So, planning should proceed with two tracks:
1. **Primary discovery track with Escola**
   - Ask Escola/school for developer documentation specifically covering custom-tool API access, webhooks, auth model, and rate limits.
2. **Fallback delivery track (if no custom API)**
   - Use Teams-based timed/event notifications driven by your own workflow engine and data deltas from imports/exports.

## If no custom-tool API is available: Teams push strategy
If Escola only provides synchronization/export-style interfaces, then:
- Use scheduled jobs (e.g., daily/weekly) to process progress deltas.
- Push teacher-approved parent updates via Teams channels/workflows used by staff.
- Add throttling rules (quiet hours, duplicate suppression, max-per-day).
- Keep an audit trail (who approved/sent each notification and when).

## Suggested next vendor questions (short list)
1. Do you provide a documented API for third-party custom apps? (yes/no + docs)
2. Are webhooks/events available for grades, attendance, incidents, or messages?
3. Is Microsoft SDS one-way or bi-directional in your setup?
4. Which exact entities can be imported/exported on the customer tenant?
5. What authentication model is available for external integrations?
