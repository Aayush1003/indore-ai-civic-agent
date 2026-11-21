# Indore Civic Agent

An open-source, human-supervised civic service platform for residents and the teams that resolve local problems in Indore. The goal is to turn a clear report into a correctly routed, trackable case—not to pretend that an AI can repair a road, dispatch a crew, or replace a public authority.

## What this project is building

A resident should be able to report a problem in Hindi or English, with a description, optional location and optional photo; receive a case number; see who is responsible and what happens next; and confirm whether the issue was actually resolved. Staff should get a concise, deduplicated, location-aware work queue rather than an unstructured pile of messages.

Initial problem areas to validate with residents and municipal teams:

- Waste collection misses, overflowing bins, and missed or unclear segregation service.
- Water supply interruptions, suspected leaks, drainage problems, and waterlogging.
- Damaged roads, unsafe crossings, and traffic obstructions.
- Local smoke, dust, and other environmental complaints.
- Public-service access barriers, including language and accessibility needs.

These are product hypotheses, not a claim that we have measured or ranked Indore's current problems. The first deployment should be chosen with local residents and the responsible departments using verified case data.

## A practical, future-facing first release

1. **Report:** responsive web form; Hindi/English; optional photo and precise location; anonymous reporting where permitted; clear consent and data-retention notice.
2. **Triage:** AI suggests a category, urgency, and likely department, with a confidence score and explanation. Low-confidence, safety-sensitive, or ambiguous reports go to a human reviewer.
3. **Coordinate:** identify likely duplicate reports and group them into a map-based cluster without discarding individual case IDs. Never claim an official integration until it is authorized and working.
4. **Track:** show received, under review, assigned, in progress, and resolved states, with timestamps and a plain-language next step. A human or verified system must confirm status changes.
5. **Verify:** request resident confirmation where practical; allow a reopened case; measure resolution and repeat incidents, not just reports received.
6. **Learn safely:** publish aggregated service trends and anonymized hotspots. Do not expose complainants, exact home locations, faces, or unredacted photos.

## Start small, then prove it works

Pilot one willing ward or service team and one or two workflows—such as missed waste pickup and water/drainage complaints. Map the real intake and escalation process before building integrations. Test with residents, field staff, and accessibility needs; keep a manual fallback; and expand only after the team can meet agreed service targets.

## Project blueprint

See [`docs/INDORE_CIVIC_BLUEPRINT.md`](docs/INDORE_CIVIC_BLUEPRINT.md) for pilot scope, workflows, data model, AI safeguards, evaluation metrics, and a staged roadmap. It deliberately separates verified facts from assumptions and lists official data sources that must be checked before use.

## Current status

This repository is at the product-design stage. It does not yet provide a deployed service, a working AI model, live municipal integrations, or verified real-time Indore data. Contributions should start with the smallest usable, privacy-conscious pilot and document what has actually been tested.

## Principles

- **Human accountability:** AI assists with classification and drafting; people and authorized systems make consequential decisions.
- **No false promises:** show a tracking ID and honest status; do not imply a report was filed with a government system unless it was.
- **Privacy by default:** collect only what is needed, restrict access, redact media, and set a retention policy before launch.
- **Inclusive access:** Hindi and English from the start, mobile-first design, accessible controls, and a non-digital fallback through a partner service desk.
- **Open and measurable:** document integrations, publish aggregate outcomes, and make errors and limitations visible.

## Contributing

Before proposing a citywide feature, help validate the workflow with the residents and staff who would use it. See the blueprint for the first pilot questions and the data that must be verified. No personal resident data or real complaint photos should be committed to this repository.
