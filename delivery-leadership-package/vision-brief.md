# Evergreen Quote: Vision Brief


## Product
**Name:** Evergreen Insurance Quote (the launch: full-stack delivery)
**Delivery week:** Final
**Delivery Lead:** Patricia Mengi
**Engineering team (represented by):** https://github.com/asc1-student09/evergreen-quote-launch
**GitHub Project board:** https://github.com/users/asc1-student09/projects/5/views/1?layout_template=board

## Who is the customer?

The customer is a first-time insurance shopper who is comparing options online, often on a phone and under time pressure, and wants a believable monthly premium before leaving for a competitor. Today, they move between a marketing page, a generic estimate tool, and later conversations with an agent, forcing them to restart or re-enter information each time they return.

## What pain does Evergreen Quote remove?

Uncertainty. The shopper cannot tell whether the price they see is real, whether it will still exist when they return, or whether an agent can access the same information later. Evergreen Quote makes the estimate immediate, saved, and consistent. The customer gets a quote, can return to it later, and an agent can retrieve the same quote without requiring the customer to repeat information. The result is a smoother, more trustworthy path to a buying decision.

## What does "good" look like at end of the week?

- A shopper enters quote details and sees a live premium without leaving the page.
- A saved quote remains available after refresh and is retrieved from the API.
- The premium displayed in the browser matches the premium stored by the API for the same inputs.
- An agent can retrieve that quote through a GraphQL query with only the fields needed.
- The API runs in a Docker container on a local Kind cluster, and CI is green on the main branch.

## What are we explicitly NOT doing this week?

- Redesigning the entire insurance product or business model.
- Building a full customer account or policy-management system.
- Adding coverage types or underwriting rules beyond the launch requirements.
- Not deploying to AWS (except for the optional Thursday cloud window if the instructor opens it).


## How will we know if it worked?

- A stakeholder walks the full quote flow (quote, refresh, agent lookup) on Thursday with no help.
- A quote is successfully persisted and retrieved through the API.
- CI stays green on main all week, with any red fixed the same day.
- The browser makes a real API call and the quote is persisted to the database.
- The client and API both pass CI before the PR is merged.
- The full stack is demo-ready and working end-to-end for Friday’s showcase.
