# Delivery Lead Notes

## Day 1 (Mon): Observations

### 1. The data gap (top risk)

The API serves six quotes from MongoDB (IDs `q1`–`q6`). The website shows five quotes from its own sample data and never calls the API. A quote saved in the browser disappears on reload. The page estimates, and the service stores quotes. The two are still disconnected.

### 2. Rate mismatch

The client estimated $425.00/month for Auto coverage, age 35, and $50,000 in coverage. The API uses a different rate table. The sponsor directed me to align the client rates to the API rates.

## Day 2 (Tue): Observations

### 1. Client and API connected

Wired the client to the API through the Vite proxy and retired the static quote files (`sampleQuotes.ts` and `quotes.json`) with `git rm`. The Recent quotes panel showed `q1`–`q6` from MongoDB. A saved quote survived a browser reload.

### 2. The type-check caught a field mismatch

The client type-check reported that `id` does not exist on `ApiQuote`. The API sends `_id`, so I updated the code that reads the response from `doc.id` to `doc._id`. The API response format stayed the same.

### 3. Launch rates aligned

Before the change, the Auto quote for age 35 and $50,000 in coverage showed a $425.00/month estimate and saved at $450.00/month. I aligned the client rates in `premium.ts` to the API rates. The estimate and saved premium then both showed $450.00/month. The API is the source of truth for pricing.

### 4. Launch configuration applied

The client title in `client/.env` is “Evergreen Insurance - Instant Quote.” The landing banner is “Evergreen Quote Insurance,” and both quote links point to `http://localhost:5173`.

### 5. GraphQL mutation verified

A Life quote for age 30 and $100,000 in coverage returned `monthlyPremium: 700`. GraphQL saved the quote to the same MongoDB database used by the REST API.

### 6. Database records verified

`db.quotes.find()` showed six seeded quotes, two saved Auto quotes at $450/month with UUIDs, and one GraphQL Life quote at $700/month. Every record had an `_id`.

### 7. Inject #1 — Launch scope

I approved the life-first landing hero copy and routed the request to change the form default to engineering. I deferred Renters coverage until after launch because adding it affects both client and database validation. The demo plan uses the local `evergreen` kind cluster, `kubectl port-forward svc/evergreen-quote-api 3000:80`, and the client at `http://localhost:5173`.

### Journey check

TypeScript checked the `ApiQuote` response format and caught the `id` versus `_id` mismatch before the app ran. I fixed how the client reads the response. Mongoose enforces the allowed coverage types (`auto`, `home`, and `life`) when the API saves a quote. Adding Renters would require updates in both places.

## Day 3 (Wed): Observations

### 1. The API ran in Docker

I built and ran `evergreen-quote-api:2.0`. The container connected to MongoDB on the VM, and the client still showed the existing quotes after the switch.

### 2. The app worked on the local Kubernetes cluster

I reused the local `evergreen` kind cluster. After deployment, all three API pods and the MongoDB pod showed `1/1 Running`. Port forwarding let the client keep reaching the API on port `3000`. The health check returned `status: ok`.

### 3. A saved quote survived a reload

I saved a Life quote through the Kubernetes API and confirmed it still appeared under Recent quotes at $700/month after refreshing. The VM and Kubernetes use separate MongoDB databases. I recorded the result in R3 of the risk register and kept the check for sample data before Friday’s demo.

### 4. Both CI jobs passed

GitHub Actions passed the API tests with a clean test database and passed the client TypeScript check and build. [Successful GitHub Actions run](https://github.com/asc1-student09/evergreen-quote-launch/actions)

### 5. Inject #2 — Shared demo incident

The shared demo API kept restarting, and the page could not load recent quotes. Its MongoDB pod was running. The deployment supplied `MONGO_URI`, while the API expected `MONGODB_URI`. My local `evergreen` cluster passed its health check, and a quote saved through that cluster was still visible after refreshing.

**Draft to the platform team**

The API on the shared demo cluster is restarting and trying to connect to MongoDB at its own address. The deployment shows `MONGO_URI`, while the API expects `MONGODB_URI`. Can your team confirm the mismatch, restore the expected setting, and share an ETA by the 3:30 check-in?

**Draft to the manager**

Thanks for flagging the recent-quotes error. Friday’s demo is still on track using my local Kubernetes cluster, where I verified that a quote can be saved and retrieved. I’ll follow up with the platform team on the shared demo environment and update you at the 3:30 check-in.

### Journey check

The client kept sending API requests through the Vite proxy to port `3000`. The dev server and standalone Docker container each listened there. For Kubernetes, port forwarding connected that same local port to the Kubernetes Service. The API kept the same routes and response format, so the client worked without a code change. Phase 3’s API and MongoDB work built the service and its storage. Docker packaged the API, and Kubernetes ran three copies behind one Service.