# Apollo.io (apollo-enrich)

Apollo.io is a sales intelligence and engagement platform built on a B2B database of hundreds of millions of contacts and companies. Its REST API exposes **People Enrichment** (single and bulk match), **People Search**, **Organization Enrichment and Search**, **Contacts** and **Accounts** management, and **Sequences** (emailer campaigns) for outreach - covering contact discovery, data enrichment, prospecting, and sales intelligence use cases.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/apollo-enrich/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/apollo-enrich/refs/heads/main/apis.yml)

## Access model (read this first)

Apollo's API is real and documented, but it is **not free or open**. Access is gated by plan and by credits:

- **API access is unavailable on the Free and Basic plans.** On those tiers every interaction is manual in the app - there is no programmatic access.
- **Programmatic API access begins on the Professional plan** (~$79/user/month annual) and continues on Organization and custom Enterprise plans.
- **Authentication is via an `x-api-key` header** on every request. Some endpoints - notably **People Search** - require a key that has been marked as a **master key**.
- **Data actions consume Apollo credits** (email, mobile, export). People Enrichment consumes credits per enriched record returned; People/Organization Search consume credits per page returned.
- **Rate limits are fixed-window and vary by plan.** Read your account's current per-minute/hour/day limits from the API usage stats endpoint or the developer dashboard at [developer.apollo.io](https://developer.apollo.io).

Because of this gating, the endpoints documented here are grounded against Apollo's public reference at [docs.apollo.io](https://docs.apollo.io) but exercising them requires a paid, API-enabled plan and a valid key.

- **Base URL:** `https://api.apollo.io/api/v1`
- **Auth header:** `x-api-key: YOUR_API_KEY`

## Tags

- Contact Discovery
- Data Enrichment
- Sales Intelligence
- B2B Data
- Prospecting
- Web Intelligence
- Lead Generation
- People Search

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Apollo People Enrichment API

Enrich a single person (`POST /people/match`) or up to ten people in one call (`POST /people/bulk_match`) - resolving names, titles, employment, verified work emails, and (with reveal flags) personal emails and phone numbers. Consumes Apollo credits per enriched record when data is returned.

- **Human URL:** [https://docs.apollo.io/reference/people-enrichment](https://docs.apollo.io/reference/people-enrichment)
- **Base URL:** `https://api.apollo.io/api/v1`

### Apollo People Search API

Find prospects across Apollo's B2B database (`POST /mixed_people/api_search`) with filters for job titles, seniorities, locations, company attributes, technologies, and email status. Paginates up to 50,000 records (100 per page, up to 500 pages). Requires a master API key; does not return emails or phone numbers - pair with enrichment to reveal contact details.

- **Human URL:** [https://docs.apollo.io/reference/people-api-search](https://docs.apollo.io/reference/people-api-search)
- **Base URL:** `https://api.apollo.io/api/v1`

### Apollo Organization Enrichment API

Enrich one company by domain, name, LinkedIn, or website (`GET /organizations/enrich`) or up to ten at once (`POST /organizations/bulk_enrich`), returning firmographics such as industry, employee count, revenue, location, and technologies.

- **Human URL:** [https://docs.apollo.io/reference/organization-enrichment](https://docs.apollo.io/reference/organization-enrichment)
- **Base URL:** `https://api.apollo.io/api/v1`

### Apollo Organization Search API

Search Apollo's company database (`POST /mixed_companies/search`) with filters for domains, employee count, location, revenue, technology stack, funding, and active job postings. Paginates up to 50,000 records; consumes credits per page when data is returned.

- **Human URL:** [https://docs.apollo.io/reference/organization-search](https://docs.apollo.io/reference/organization-search)
- **Base URL:** `https://api.apollo.io/api/v1`

### Apollo Contacts API

Manage contacts saved inside your Apollo account - search (`POST /contacts/search`), create (`POST /contacts`), update (`PUT /contacts/{id}`), and bulk-create contacts, plus list contact stages. Contacts are the people you have added to Apollo, distinct from raw database search results.

- **Human URL:** [https://docs.apollo.io/reference/search-for-contacts](https://docs.apollo.io/reference/search-for-contacts)
- **Base URL:** `https://api.apollo.io/api/v1`

### Apollo Accounts API

Manage accounts (companies saved to your Apollo team) - search (`POST /accounts/search`), create (`POST /accounts`), update (`PUT /accounts/{id}`), and bulk-create accounts. Accounts are the company records your team tracks, distinct from the broader organization database.

- **Human URL:** [https://docs.apollo.io/reference/search-for-accounts](https://docs.apollo.io/reference/search-for-accounts)
- **Base URL:** `https://api.apollo.io/api/v1`

### Apollo Sequences API

Drive multi-step outreach through Apollo sequences (emailer campaigns) - create and search sequences and add contacts to a sequence (`POST /emailer_campaigns/{id}/add_contact_ids`), plus draft, send, and search outreach emails. Turns discovered and enriched contacts into active engagement.

- **Human URL:** [https://docs.apollo.io/reference/add-contacts-to-sequence](https://docs.apollo.io/reference/add-contacts-to-sequence)
- **Base URL:** `https://api.apollo.io/api/v1`

## Common Properties

- [Authentication](authentication/apollo-enrich-authentication.yml)
- [GitHub Organization](https://github.com/apolloio)
- [LinkedIn](https://www.linkedin.com/company/apolloio)
- [Website](https://www.apollo.io)
- [Documentation](https://docs.apollo.io)
- [Developer Portal](https://developer.apollo.io)
- [Plans](plans/apollo-enrich-plans-pricing.yml)
- [Pricing](https://www.apollo.io/pricing)
- [Rate Limits](rate-limits/apollo-enrich-rate-limits.yml)
- [Fin Ops](finops/apollo-enrich-finops.yml)

## WebSocket review

Apollo does **not** expose a documented public WebSocket API. The entire public surface is request/response REST over HTTPS with an `x-api-key` header; asynchronous enrichment results (phone reveal, waterfall) are delivered to a consumer-supplied `webhook_url`, which is an HTTP callback, not a WebSocket. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
