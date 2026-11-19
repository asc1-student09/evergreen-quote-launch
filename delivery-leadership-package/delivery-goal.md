# Delivery Goal: Evergreen Quote



## Goal

By Thursday EOD, the wired Evergreen Quote app saves quotes that survive a reload, the containerized API has run on the local cluster, and the launch is merged to main via a reviewed PR with both CI jobs green.

## "Done" looks like

- The quote page loads its recent quotes from the API, and a saved quote survives a reload.
- The estimate on screen and the saved premium agree, at the launch rates.
- `npm test` (API) and `npm run type-check` + `npm run build` (client) pass; both CI jobs on the merge commit are **green**.
- The containerized API serves the wired app, and the cluster demo shows three API pods behind one Service.
- The landing page carries the launch banner and points at the app.
- A reviewed PR is merged, branch deleted.
- `delivery-leadership-package/` is complete and committed.

## Out of scope (this week)

- Redesigning the entire insurance product or business model.
- Building a full customer account or policy-management system.
- Adding coverage types or underwriting rules beyond the launch requirements.
- Not deploying to AWS (except for the optional Thursday cloud window if the instructor opens it).
