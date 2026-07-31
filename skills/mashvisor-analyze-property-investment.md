---
name: Analyze a property investment with Mashvisor
description: Look up a property and pull its full rental-investment analysis (cap rate, cash flow, ROI) for both Airbnb and traditional strategies.
api: openapi/mashvisor-openapi.yml
operations: [getProperty, getPropertyInvestment, getPropertyInvestmentBreakdown]
---

# Analyze a property investment with Mashvisor

Use the Mashvisor Data API to evaluate a single property as a rental investment.

## Auth
- Base URL: `https://api.mashvisor.com/v1.1`
- Send your key in the `x-api-key` header on every request.
- Almost every call requires a two-letter `state` (path or query). Omitting it returns 404.

## Steps
1. **Find the property** — `getProperty` (`GET /client/property?state={ST}&address=...` or `&zip_code=...`/`&mls_id=...`). Capture the property `id` (`pid`) from the response.
2. **Get the investment analysis** — `getPropertyInvestment` (`GET /client/property/{id}/investment?state={ST}`). Optionally pass `down_payment`, `interest_rate`, `loan_type`, `airbnb_rental`, `traditional_rental` to model financing assumptions. Read cap rate, cash flow, and ROI for both Airbnb and traditional.
3. **Break down the numbers** — `getPropertyInvestmentBreakdown` (`GET /client/property/{id}/investment/breakdown?state={ST}`) for the detailed cost/return breakdown (startup cost, recurring, turnover).

## Conventions
- Responses are JSON: `{ "status": "success", "content": { ... } }`.
- Errors: `{ "status": "error", "code": <http>, "message": <text> }` (see errors/mashvisor-problem-types.yml). 401 = bad key, 429 = over rate/quota.
- Read-only; safe to retry.
