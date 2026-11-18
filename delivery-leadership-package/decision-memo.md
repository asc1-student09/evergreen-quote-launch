# Decision Memo: Where the premium calculation lives

**Date:** November 18, 2026
**Author:** Patricia Mengi, Delivery Lead
**Decision area:** Premium pricing calculation and the Evergreen Quote launch

## Context

The website estimates a customer's premium immediately, while the API calculates the premium that is saved. On Day 2, the same quote showed $425 estimated on the website but $450 saved by the API because the two sets of rates differed. Per the sponsor's direction that "the server is the source of truth," I aligned the website rates to the API rates. Both now show $450. The calculation remains in two places, and a future rate change could create the same problem again. Launch is Friday, November 20.

## Options considered

1. **Option A: Keep both calculations and update them together.** This preserves a fast estimate and is the lowest-risk option for the current week. However, two lists of rates remain, so a person must maintain both carefully.
2. **Option B: Make every estimate call the API.** This creates one source of truth and reduces the chance of disagreement, but every estimate needs a working server and may take slightly longer.
3. **Option C: Keep the current setup for launch, then move to one shared rate source.** This avoids launch-week risk but defers the maintenance problem until afterward.

## Recommendation

Choose Option A for launch and plan to move to Option C after launch.

## Why

Customers should receive an instant estimate that matches the premium they are shown after saving. Keeping both calculations aligned for Friday avoids making a risky architecture change immediately before launch. After Friday, the team can centralize the rates with less schedule pressure.

## What would change my mind

If the website and saved premium disagree again before Friday, or if the approved rates change before launch, I would use Option B instead. The API is the authority, so making every estimate a server calculation would be safer than shipping a second possible wrong answer.
