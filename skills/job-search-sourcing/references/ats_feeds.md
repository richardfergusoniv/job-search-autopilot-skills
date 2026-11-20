# ATS feeds: starter directory

Public JSON endpoints for employer job boards. No authentication, no API key. `{slug}` is the board slug from the company's careers-page URL.

This directory is a starting point, verified against the live endpoints in late 2026. It skews toward technology, venture capital, finance, and real estate employers, because that is where it was built. Treat every entry as a strong lead, not a guarantee: boards move, and the health check in the sourcing skill is what keeps the user's own copy honest. Extend the copy, never this original: when the user's Muse wires a new company, it adds the row to the user's directory and reports the build under the setup document's status report rules.

## Endpoint patterns

| ATS | Endpoint |
| --- | --- |
| Greenhouse | `https://boards-api.greenhouse.io/v1/boards/{slug}/jobs?content=true` |
| Lever | `https://api.lever.co/v0/postings/{slug}?mode=json` |
| Ashby | `https://api.ashbyhq.com/posting-api/job-board/{slug}?includeCompensation=true` |
| SmartRecruiters | `https://api.smartrecruiters.com/v1/companies/{slug}/postings` |
| Workable | `https://apply.workable.com/api/v1/widget/accounts/{slug}?details=true` |
| Recruitee | `https://{slug}.recruitee.com/api/offers/` |
| Personio | `https://{slug}.jobs.personio.de/xml` |
| Breezy HR | `https://{slug}.breezy.hr/json` |
| Pinpoint | `https://{slug}.pinpointhq.com/postings.json` |
| Rippling | `https://api.rippling.com/platform/api/ats/v1/board/{slug}/jobs` |
| Workday | `https://{tenant-host}.myworkdayjobs.com/wday/cxs/{tenant}/{site}/jobs` (POST; tenant host includes the shard, for example `wd5` or `wd503`) |
| Teamtailor | `https://{career-site-host}/jobs.rss` |

## Verified starter feeds

| Company | ATS | Slug or config |
| --- | --- | --- |
| Airbnb | Greenhouse | `airbnb` (the API returns country-level locations; the real location is on each posting page) |
| Affirm | Greenhouse | `affirm` |
| Andreessen Horowitz | Greenhouse | `a16z` |
| Anthropic | Greenhouse | `anthropic` |
| Carta | Greenhouse | `carta` |
| DivcoWest | Greenhouse | `divcowest` |
| KKR | Greenhouse | `stage` (reachable only through boards-api; the public board page 404s) |
| Knock | Greenhouse | `knock` |
| Rexford Industrial | Greenhouse | `rexfordindustrial` |
| TPG | Greenhouse | `tpgcareers` |
| AngelList | Lever | `angellist` |
| 8VC | Ashby | `8vc` |
| Allocate | Ashby | `allocate` |
| Arch | Ashby | `arch` |
| Forerunner | Ashby | `forerunner` |
| Hudson Pacific Properties | Ashby | `hudson-pacific-properties` |
| Lightspeed | Ashby | `lightspeed` |
| OpenAI | Ashby | `openai` |
| Perplexity | Ashby | `perplexity` |
| Sequoia Capital | Ashby | `sequoia` |
| Extra Space Storage | Workday | tenant `extraspace`, shard `wd5`, site `ESS_External` |
| Ventas | Workday | tenant `ventas`, shard `wd503`, site `ventas_careers` |
| American Tower | Oracle HCM | host `hdsn.fa.us6.oraclecloud.com`, site `CX_1` (the careers domain is a vanity proxy; resolve the real host from its redirect) |
| Crown Castle | UKG | `recruiting2.ultipro.com/CRO1010CCUSA/JobBoard/74c30440-80fa-4099-8981-2e10b7193d27` |
| Regency Centers | Dayforce | namespace `regency`, portal `CANDIDATEPORTAL` |

## Checked, no public feed

These employers were probed across the major ATS platforms and had no wireable public feed at check time. Do not burn runs re-probing them without a reason; cover them with the keyword layer and browser checks instead: Addepar, Alexandria Real Estate Equities, Align Real Estate, Allocations, Anduin, Arrived, Assure, Broadreach Capital Partners, BXP, Carmel Partners, Cousins Properties, CubeSmart, Douglas Emmett, EastGroup Properties, EPR Properties, Flow, Four Corners Property Trust, GI Partners, GlassRatner, Hamilton Zanze, Harvest Properties, Healthpeak, Iron Mountain, Jay Paul Company, Kilroy Realty, Kimco Realty, Lane Partners, Masttro, Opendoor, Paramount Group, PCCP, PeerStreet, Prado Group, RealtyMogul, Redfin, Sares Regis, Shine Associates, Shorenstein, SL Green, STAG Industrial, Stockbridge, Terreno Realty, Tishman Speyer, TMG Partners, Veritas Investments, VICI Properties, Weyerhaeuser, Yieldstreet, Zillow.

Prologis and Blackstone run on Workday, whose edge drops non-browser clients: browser checks only, no scripted feed.

## Adding a company

1. Open the company's official careers page and identify the ATS from the URL pattern (the board domain or slug is usually visible in the address or the page source).
2. Probe candidate slugs against the matching pattern above: lowercase, hyphenated, suffix-stripped variants (drop "Inc," "Labs," and similar), until one returns a valid board.
3. Identity-verify before wiring: the postings' own text must name the company (boilerplate, about text, or job content). A board that returns HTTP 200 with zero jobs cannot be attributed to the company; do not wire it, however plausible the slug looks.
4. Record the row in the user's directory with the date verified. If no ATS yields a feed, record that too, so the probing is not repeated next quarter.
