# Apollo.io (apollo-enrich)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
