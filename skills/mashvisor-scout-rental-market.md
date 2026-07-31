---
name: Scout a rental market with Mashvisor
description: Rank the best neighborhoods and rental-rate estimates in a city to find where to invest.
api: openapi/mashvisor-openapi.yml
operations: [listTopMarkets, listCityNeighborhoods, getRentalRates, getTrendsSummary]
---

# Scout a rental market with Mashvisor

Use the Mashvisor Data API to survey a market before drilling into individual properties.

## Auth
- Base URL: `https://api.mashvisor.com/v1.1`, `x-api-key` header, `state` required.

## Steps
1. **Find the hot markets** — `listTopMarkets` (`GET /client/city/top-markets?state={ST}`) to rank cities in the state.
2. **List the neighborhoods** — `listCityNeighborhoods` (`GET /client/city/neighborhoods/{state}/{city}`).
3. **Pull rental-rate estimates** — `getRentalRates` (`GET /client/rental-rates?state={ST}&city=...&source=airbnb|traditional`) for estimates by bedroom count with comparable sample counts.
4. **Check market trends** — `getTrendsSummary` (`GET /client/trends/summary/{state}/{city}`) for the market-trends summary.

## Conventions
- Paginated list endpoints accept `page` and `items`.
- JSON success envelope `{ "status": "success", "content": {...} }`; errors carry `status`/`code`/`message`.
