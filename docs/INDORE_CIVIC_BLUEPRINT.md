# Indore Civic Agent: product blueprint

**Status:** proposal for a locally validated pilot; not an official Indore Municipal Corporation service.

This document is a practical starting point, not a claim to have conducted field research or accessed live city datasets. Validate every workflow, responsible office, service commitment, and data source with Indore residents and authorized staff before launch.

## 1. The civic problem to solve

Civic reports often arrive through disconnected channels and in different formats. Residents may not know which office to contact or whether anyone acted; staff may receive duplicate or incomplete reports without a location they can use. An AI front end is useful only if it improves the handoff and follow-through.

The platform's job is to make each report **actionable, accountable, and trackable**. It is not a substitute for emergency services, municipal authority, field inspection, or official grievance procedures.

### Needs to test locally

Treat these as candidate workflows to investigate—not as a data-backed ranking of Indore's problems:

| Candidate workflow | Useful report details | Possible triage assistance |
| --- | --- | --- |
| Missed waste pickup / overflowing public bin | Approximate location, date/time, optional bin or lane photo | Distinguish missed collection from bulk waste or a public-bin overflow; detect nearby duplicate cases |
| Water leak / drainage / waterlogging | Location, when observed, whether still active, optional photo | Separate suspected leak from blocked drain or standing water; flag reports near one another |
| Road damage / obstruction / unsafe crossing | Location, affected direction or landmark, whether a route is blocked | Suggest category and route obstruction urgency for human review |
| Smoke, dust, or local pollution concern | Location, time, duration, optional safe-distance photo | Group time-and-place reports; never infer a confirmed source or exposure level from a photo |
| Difficulty accessing a civic service | Service sought, preferred language/contact method, optional details | Find the appropriate verified information or human referral; do not invent eligibility or deadlines |

Do not start with automated enforcement, predictive policing, citizen scoring, facial recognition, or automated denial of services. They are outside the pilot's purpose and create disproportionate risks.

## 2. First pilot: one service, one team, one small area

Select the pilot area with local partners based on willingness to participate, a clear service owner, a usable manual escalation path, and the ability to measure outcomes. Do not choose a ward based on assumptions about residents or publish comparative ward rankings without context.

Before accepting public reports, answer these questions with the partner team:

- Which existing channel currently accepts this kind of complaint, and can this project lawfully and reliably hand it off?
- Who owns intake, assignment, field work, status updates, and closure?
- Which fields are genuinely needed to act? Can a report be made without a name or exact home address?
- What response and update expectations can the partner actually meet? Publish only commitments approved by the service owner.
- How are urgent hazards redirected, and what happens outside staffed hours?
- How can a resident without a smartphone or internet use the same process?
- What retention period, access controls, and deletion process apply to reports and attachments?

If no authorized system integration exists, use a clearly disclosed pilot queue reviewed by the partner. Never tell a resident that an official complaint was filed when it was only recorded in this project.

## 3. Resident-to-resolution workflow

1. **Create a report.** Offer Hindi and English, plain-language prompts, keyboard and screen-reader access, and a mobile-friendly experience. Description is required; exact GPS and photos are optional. Let the resident choose a landmark or approximate pin instead of sharing their home location.
2. **Confirm understanding.** Show a short summary, selected category, location precision, and consent before submission. Allow the resident to correct the AI's suggested category.
3. **Issue a receipt.** Create a random case identifier and explain where the case will be seen, who can access it, how to check status, and how to request deletion or correction where applicable.
4. **Triage with a person in control.** The model may suggest a category, duplicate candidates, and a concise translation or summary. Display confidence and the original text. A person reviews low-confidence cases, sensitive content, urgency, and assignment.
5. **Route and update.** Assign only to a verified team or to a transparent manual queue. Record who or what changed the case state and when. If routing fails, say so and provide the approved alternative channel.
6. **Resolve and verify.** An authorized staff member records the action and evidence appropriate to the workflow. Invite resident confirmation where possible. Keep “work marked complete” distinct from “resident confirmed”; allow reopening.
7. **Learn from aggregates.** Publish counts and service-time distributions only after removing identifiers and checking that small groups or precise locations cannot expose a reporter.

### Status vocabulary

`Received` → `Needs review` → `Assigned` → `In progress` → `Action recorded` → `Closed`

A case may be `Reopened` or `Unable to route`. Show an explanation and next step for every status. “Closed” must not silently mean “the AI thinks it is fixed.”

## 4. Minimal data model

Keep personal contact details separate from the operational case wherever possible.

- **Case:** random ID, created time, resident's original description, selected category, status, status history, language, and optional accessibility/contact preference.
- **Location:** optional coordinates or landmark, precision level, and the resident's consent to use the location for routing. Avoid storing a more precise location than the task needs.
- **Attachment:** optional media, access restrictions, redaction state, retention deadline, and deletion state. Strip image metadata such as embedded GPS before storage or publication.
- **Triage suggestion:** model/version, suggested category and summary, confidence, timestamp, and human acceptance or correction. Do not treat generated text as ground truth.
- **Assignment/action:** verified receiving team, actor, timestamps, action note, and source of each update (staff, resident, or authorized integration).
- **Audit event:** append-only record of access and state changes, with role-based access and no unnecessary copies of sensitive report text.

A production implementation still needs a threat model, security review, legal/privacy review, access-control design, backup/deletion plan, and a published retention schedule.

## 5. AI boundaries and safeguards

**Appropriate pilot uses:** category suggestions, duplicate candidates for human confirmation, translation drafts, plain-language summaries, and retrieval of answers from an approved, maintained information source.

**Not appropriate:** deciding that a report is false, identifying a person from an image, inferring a resident's identity or intent, automatically dispatching crews, determining legal eligibility, promising a service deadline, or closing a case without authorized evidence.

Required safeguards:

- Display model uncertainty; provide a non-AI/manual path for every workflow.
- Preserve the original report and make AI edits or translations visibly distinguishable.
- Require human review before routing sensitive cases or making consequential changes.
- Test Hindi and English performance with locally reviewed examples, including spelling variation and code-mixing; provide a way to report translation errors.
- Prevent prompt-injected report text from changing system instructions or triggering external actions. Treat user text and uploaded media as untrusted input.
- Do not send resident data to model providers until their retention, training, residency, and access terms are reviewed and disclosed.
- Log model version and human corrections; periodically check error rates by language and category. Pause a model feature if it causes harmful misrouting.

## 6. Data and integration research checklist

No live source is integrated by this proposal. Before building any integration, confirm that the source exists, is current, covers the pilot area, permits the intended use, has stable access, and has a named operational owner. Candidate places to investigate with official partners include:

- Indore Municipal Corporation (IMC) public service information and authorized grievance/work-order channels.
- Madhya Pradesh e-Nagar Palika services, if a relevant, documented interface is available and the responsible authority approves its use.
- Madhya Pradesh Pollution Control Board and Central Pollution Control Board published air-quality information, after checking station coverage, timestamps, licensing, and limitations.
- India Meteorological Department forecasts and warnings for weather context, with the original issue time and source shown.
- Publicly released ward boundaries, roads, drainage, waste-service schedules, and traffic information, only where licensing and update quality are clear.

Do not scrape private systems, bypass access controls, or represent a nearby sensor/forecast as a measurement at a resident's exact location. Display source, timestamp, spatial coverage, and stale-data warnings for every feed.

## 7. Measures of success

Agree baselines and targets with the service owner before launch. Report denominators and time windows; do not optimize for report volume alone.

- Share of reports with enough information to route, and share needing manual correction.
- Time from submission to first meaningful status update and to assignment.
- Time to recorded action, separated by category and operating hours.
- Duplicate handling accuracy and cases incorrectly merged or split.
- Resident-confirmed resolution rate, reopen rate, and repeat reports at the same approximate location.
- Misrouting, translation, and urgency-triage error rates from human review.
- Completion rates and usability feedback by language and accessibility needs, collected with consent.
- Privacy/security incidents, deletion requests completed, and reports with no successful handoff.

Publish aggregated results and known limitations. Do not publicly expose raw complaints, contact details, exact household coordinates, or staff performance rankings derived from unverified case data.

## 8. Staged roadmap

### Stage 0 — Discovery

Interview residents, field workers, and service owners; map one existing workflow; verify the escalation path and candidate data; agree privacy and retention requirements; document a non-digital fallback. No AI or public intake is required yet.

### Stage 1 — Usable manual pilot

Deliver an accessible Hindi/English report form, case receipt, human-operated queue, auditable status history, and basic aggregate metrics for one selected workflow. Test with synthetic data before handling real cases.

### Stage 2 — Bounded AI assistance

Add opt-in internal category/summary suggestions and duplicate candidates. Compare against human review, measure language-specific errors, and retain a manual-only switch. Do not automate external actions.

### Stage 3 — Authorized integration

Only after written operational approval and a working sandbox, connect the chosen official channel. Add retries, idempotency, clear failure states, reconciliation, and tests for duplicate submissions. Keep the resident-facing receipt honest about which system accepted the case.

### Stage 4 — Evidence-led expansion

Expand to another service or area only when the pilot demonstrates safe routing, useful status updates, manageable workload, and a functioning deletion/security process. Revalidate each new service's owner, workflow, and metrics.

## 9. Definition of a responsible launch

A pilot is ready for public use only when there is a named service owner, tested report-to-human handoff, approved public wording, Hindi/English and accessibility checks, privacy notice and retention schedule, restricted staff access, incident and outage procedures, a non-digital alternative, synthetic-data tests, and a way to correct or reopen a report. If any of these are missing, label the system as a demo and do not accept real personal data.
