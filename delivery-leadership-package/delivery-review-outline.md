# Program Showcase: Evergreen Quote

**Presenter** — Patricia Mengi, Delivery Lead  
**Timing** — 5 minutes to present, followed by 3 minutes for questions

## Slide 1: Delivery goal & did we hit it?

- **Goal** — By Thursday EOD, the wired Evergreen Quote app saves quotes that survive a reload, the containerized API has run on the local cluster, and the launch is merged to main via a reviewed PR with both CI jobs green.
- **Hit?** ☒ Yes  ☐ Partially  ☐ No
- **Why** — A saved quote survived a browser refresh, the API ran on local Kubernetes, and both CI jobs passed on the reviewed merge commit on `main`.

## Slide 2: What shipped

- **Screenshot** — The PowerPoint includes the local production preview showing the quote form and the $700/month Life quote under Recent quotes.
- **Merged PR** — [Pull request #11](https://github.com/asc1-student09/evergreen-quote-launch/pull/11)
- **Green CI run** — [API tests and client type-check/build on main](https://github.com/asc1-student09/evergreen-quote-launch/actions/runs/44532674190)
- **AWS evidence** — The AWS load balancer returned the $450/month Auto quote saved on EKS. EKS and ECR cleanup were verified.
- **Optional live demo** — Open the landing page, click **Get your quote**, save a sample quote, and refresh to show it under **Recent quotes**. Use the local `evergreen` Kubernetes cluster for the live demo and the screenshots as the fallback.

## Slide 3: Two key decisions

- **Decision 1** — Keep the instant estimate for launch and align the client rates to the API rates. **Why it mattered** — The same Auto quote had shown a $425 estimate and saved at $450. After the change, both showed $450.
- **Decision 2** — Correct Copilot’s two sample premiums before keeping the rows. **Why it mattered** — Both suggested prices were valid numbers, so they could pass database validation even though they disagreed with the launch rates. After the correction, all eight sample quotes loaded successfully.

## Slide 4: Risks & injects

- **Top risk (R1)** — The website started with its own sample quotes, and a quote saved in the browser disappeared on refresh. I connected the website to the API and verified that a saved quote could be retrieved after a reload.
- **Inject #1 (Tue)** — The sponsor requested a life-first experience and Renters coverage. I approved the landing-page copy, routed the form-default change to engineering, and deferred Renters because it would change validation in both the client and API.
- **Inject #2 (Wed)** — The shared demo API pods restarted after a database configuration change. I asked the platform team to confirm the mismatch, restore the expected setting, and provide an ETA. I called **GO for Friday’s local demo** based on the local cluster health check, the saved quote that survived a refresh, and green CI.

## Slide 5: Difficulties I faced and how I handled them

- Fixed the client/API field mismatch using the TypeScript error.
- Used the lab fallback when MongoDB image import failed and cleared the local port conflict before verifying the API connection.

## Slide 6: AI use and skills growth

- Used GitHub Copilot and ChatGPT for suggestions and troubleshooting. Reviewed their output and verified the results.
- The PowerPoint includes proposed contribution estimates and before/after skill ratings for me to confirm.

## Slide 7: What I’ll bring to the way I lead

- **The journey** — Static landing page → typed React quote app → API backed by MongoDB → connected app with a containerized API running on Kubernetes.
- **What I’ll take back to work on Monday** — The biggest lesson I’m taking back to Print Services is how much clarity we can create before the work begins. On my next project, I’ll make time at kickoff for us to talk through what could get in our way and agree on when we’ll act. As a leader, I want to give the team room to surface risks early and help them get decisions while we still have options.
- **What I’d do differently** — I’d agree on a pricing check earlier so we could catch a difference between the website estimate and the saved premium as soon as either rate table changed.

## Q&A prep: likely questions

- **Why didn’t you ship Renters coverage?** It changes what both the website and the API accept. I deferred it to protect the launch scope and give engineering time to verify it end to end.
- **The demo worked. Why would one red CI job matter?** The demo proves the path I exercised. CI also checks cases the demo doesn’t cover, such as rejecting invalid quotes and producing a clean client build. A red job would hold the merge until we understood and resolved the failure.
- **Why were you comfortable calling GO during the incident?** The incident affected the shared demo cluster. I verified the local cluster planned for Friday and had screenshots ready if the live demo failed.
