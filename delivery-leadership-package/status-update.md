# Stakeholder Status Update: Evergreen Quote

**To:** Priya Ramanathan, Project Sponsor (Instructor)  
**From:** Patricia Mengi  
**Date:** November 17, 2026

## What shipped today

- Client wired to the API; stub data retired. Result: a saved quote survived a reload, a first for the program.
- Seam defect caught by the compiler and fixed (`doc.id` -> `doc._id`). Result: quotes load with valid IDs.
- Evidence: PR #11 (delivery/lead -> main): https://github.com/asc1-student09/evergreen-quote-launch/pull/11

## What slipped (and why)

- **Form default (auto -> life):** routed to the engineering team. It's one word, but it sits in shared code every estimate flows through. Small to type isn't small to ship two days before launch.

**Post-launch scope:** Renters. It spans the client, API, and two validation systems. Logged on the board.

## What's next (tomorrow)

- Patricia Mengi — before 16:00: align client rates, launch title, and landing configuration; mount GraphQL.
- Patricia Mengi — Wednesday: containerize and run on the local kind cluster `evergreen`.
- Demo plan: Friday, local on my VM; kind cluster `evergreen` (API + MongoDB), `kubectl port-forward svc/evergreen-quote-api 3000:80`, wired client at http://localhost:5173, screenshots as backup. Cloud access is not required for the required launch demo.

## What I need from you

- Approval of the life-first hero wording by **10:30 Wednesday**.

The client/API seam works today. Wednesday's priority is deployment confidence, with CI as the go/no-go gate.