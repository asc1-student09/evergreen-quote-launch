# Delivery Lead Notes

## Day 1 (Mon): Observations

### 1. The data gap (top risk)
The API (back end) serves 6 quotes from MongoDB (ids q1-q6). The website (front end) shows 5 quotes from its own stub data and never calls the API. A quote saved in the browser disappears on reload. The page estimates; the service remembers; they have never met.

### 2. Rate mismatch (for tomorrow)
The client estimated $425.00/mo for Auto, age 35, $50,000. The API's quotes use a different rate table. Sponsor rule: align the client to the API's rates.