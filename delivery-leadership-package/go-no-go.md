# Go / No-Go: Launch Decision

**Date / time:** November 18, 2026 — Day 3 sponsor check-in
**Decision:** ☒ GO   ☐ NO-GO   ☐ GO WITH CONDITIONS
**Scope:** Friday’s live demo on the local `evergreen` Kubernetes cluster

## CI evidence

- Both jobs passed on `delivery/lead`. [Successful GitHub Actions run](https://github.com/asc1-student09/evergreen-quote-launch/actions)
- Workflow file: `.github/workflows/ci.yml`
- The API job ran the route tests against a clean MongoDB test database.
- The client job ran the TypeScript check and built the production web app.

## Local demo evidence

- All three API pods and the MongoDB pod showed `1/1 Running`.
- The API health check through port `3000` returned `status: ok`.
- I saved a Life quote through the Kubernetes API and confirmed it still appeared at $700/month after refreshing the browser.
- Inject #2 affects the shared demo environment. The platform team owns that incident. Friday’s demo uses the verified local cluster.

## What "GO" means

- Proceed with Friday’s live demo on the local `evergreen` cluster.
- On Day 4, review the pull request and confirm both CI jobs pass before squash-merging `delivery/lead` into `main`. Delete the branch and tag the merge commit `launch`.

## What would trigger a "NO-GO"

- **Live demo:** If the local API fails its health check or the app cannot load the sample quote during rehearsal, switch to the screenshot fallback. I own the rehearsal check and demo decision.
- **Merge:** If either CI job fails on the pull request, hold the merge until the engineering owner resolves the failure and both jobs pass on the latest commit.
- **Re-evaluate:** Check merge readiness during Day 4 PR review and demo readiness during the Day 4 rehearsal.

## My call

GO for Friday’s live demo because I verified that the local cluster could save a quote and display it again after a browser refresh. The platform team owns the shared demo incident, and both CI jobs passed on the reviewed Day 3 run. If the local API fails its health check or the sample quote fails to load during rehearsal, I’ll use the screenshot fallback.