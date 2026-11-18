# Delivery Lead Notes

## Day 1 (Mon): Observations

### 1. The data gap (top risk)
The API (back end) serves 6 quotes from MongoDB (IDs q1-q6). The website (front end) shows 5 quotes from its own stub data and never calls the API. A quote saved in the browser disappears on reload. The page estimates; the service remembers; they have never met.

### 2. Rate mismatch (for tomorrow)
The client estimated $425.00/mo for Auto, age 35, $50,000. The API's quotes use a different rate table. Sponsor rule: align the client to the API's rates.

## Day 2 (Tue): Observations

### 1. The seam is crossed
Client wired to the API through the Vite proxy; stub data (`sampleQuotes.ts`, `quotes.json`) retired with `git rm`. The panel shows q1-q6 from MongoDB. A saved quote survived a reload—a first for the program.

### 2. The compiler caught a seam defect
type-check: "Property 'id' does not exist on type 'ApiQuote'". The API sends `_id`. Fixed the mapper (`doc.id` -> `doc._id`), not the contract.

### 3. Rate drift observed, then fixed
Before: Auto/35/50k estimate $425.00 vs. saved $450.00/mo (client 85/130/65 vs. API 90/135/70).
After aligning `premium.ts`: estimate $450.00 = saved $450.00/mo. Server is the source of truth.

### 4. Launch config applied
`client/.env` title: "Evergreen Insurance - Instant Quote". Landing banner: "Evergreen Quote Insurance"; both quote links -> http://localhost:5173.

### 5. GraphQL mutation
life/30/100k -> `monthlyPremium: 700` (launch rate 70). Same database, second contract.

### 6. Database peek
`db.quotes.find()`: 6 seeded quotes, 2 saved auto quotes ($450, UUID IDs), 1 GraphQL life quote (700). Every document carries `_id`.

### 7. Inject #1
Split the life-first ask: approved the landing hero (content I own); routed the form default to engineering (shared code, launch week). Renters deferred to post-launch (spans two validation systems). Demo plan written: kind cluster "evergreen", `kubectl port-forward svc/evergreen-quote-api 3000:80`, client at http://localhost:5173.

### Journey check
Q: Which Phase 2 topic is the "fix the mapper, not the contract" discipline, and where did a contract hold a line today?
A: TypeScript (Phase 2, Weeks 10-11). The compiler checked the `ApiQuote` contract across the client/API seam and caught `doc.id` versus `_id` before runtime; we fixed the mapper, not the contract. A second contract held: the Mongoose schema enum for `type` (`auto`, `home`, `life`) would refuse a renters quote in the database. That's TypeScript on the client and Mongoose on the server—two validation systems, which is why renters is post-launch.