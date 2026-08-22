# Dutchie (dutchie)

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

Dutchie is a cannabis retail technology platform providing point of sale, ecommerce, and payments for dispensaries. Its headless commerce product, **Dutchie Plus**, is a **GraphQL-first** API (endpoint `https://plus.dutchie.com/plus/2021-07/graphql`) that lets developers build fully custom, branded dispensary storefronts against Dutchie's ecommerce backend: query retailer menus, products, variants, potency, and specials, and drive a stateful cart/checkout that respects cannabis compliance, inventory, taxes, and per-state rules. Requests are GraphQL POST operations authenticated with a per-retailer Bearer API key.

> **GraphQL-first:** This entry is modeled with a `graphql/` directory (SDL + query guide) rather than `openapi/`, because Dutchie Plus is a GraphQL API, not REST.

> **Sunset notice:** Dutchie has announced a 2026 sunset/deprecation of the Plus headless commerce API. Confirm availability with Dutchie before building against it.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/dutchie/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/dutchie/refs/heads/main/apis.yml)

## Tags

- Cannabis
- Dispensary
- Retail
- Ecommerce
- Point of Sale
- Headless Commerce
- GraphQL
- Menu
- Checkout

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

All four logical APIs share one GraphQL endpoint (`https://plus.dutchie.com/plus/2021-07/graphql`) and Bearer (per-retailer API key) auth. Menu and Checkout operations are **confirmed** against the official [Dutchie Plus Next.js example](https://github.com/GetDutchie/dutchie-plus-nextjs-example); Retailers and Specials are **modeled** from Dutchie Plus documentation and the 2021-07 schema.

### Dutchie Plus Retailers API

GraphQL queries for the dispensaries/retailers connected to your Dutchie Plus account - retailer metadata, address, hours, order types (pickup/delivery), and pricing types (recreational/medical). The retailer scope is established by the per-retailer API key. *(Modeled.)*

- **Human URL:** [https://plus.dutchie.com/plus/docs](https://plus.dutchie.com/plus/docs)
- **Base URL:** `https://plus.dutchie.com/plus/2021-07/graphql`

#### Tags

- Retailers
- Dispensaries
- Locations
- GraphQL

#### Properties

- [Documentation](https://plus.dutchie.com/plus/docs)
- [GraphQL Guide](graphql/dutchie-graphql.md)
- [GraphQL Schema](graphql/dutchie-schema.graphql)
- [Postman Collection](collections/dutchie.postman_collection.json)
- [Open Collection](collections/dutchie.opencollection.json)

### Dutchie Plus Menu API

The core headless-storefront query. `menu(filter, pagination)` returns a retailer's live product catalog - each Product carries brand, category, strainType, description, image, CBD/THC potency, and priced variants (option, priceRec, priceMed, and special prices). *(Confirmed.)*

- **Human URL:** [https://plus.dutchie.com/plus/docs](https://plus.dutchie.com/plus/docs)
- **Base URL:** `https://plus.dutchie.com/plus/2021-07/graphql`

#### Tags

- Menu
- Products
- Variants
- Inventory
- GraphQL

#### Properties

- [Documentation](https://plus.dutchie.com/plus/docs)
- [GraphQL Guide](graphql/dutchie-graphql.md)
- [GraphQL Schema](graphql/dutchie-schema.graphql)
- [Postman Collection](collections/dutchie.postman_collection.json)
- [Open Collection](collections/dutchie.opencollection.json)

### Dutchie Plus Specials API

GraphQL queries for a retailer's active specials, deals, and promotions - the discount programs that produce the special variant prices (`specialPriceRec` / `specialPriceMed`) returned by the Menu API. *(Modeled; the special-price fields themselves are confirmed on the Product variant type.)*

- **Human URL:** [https://plus.dutchie.com/plus/docs](https://plus.dutchie.com/plus/docs)
- **Base URL:** `https://plus.dutchie.com/plus/2021-07/graphql`

#### Tags

- Specials
- Deals
- Promotions
- Discounts
- GraphQL

#### Properties

- [Documentation](https://plus.dutchie.com/plus/docs)
- [GraphQL Guide](graphql/dutchie-graphql.md)
- [GraphQL Schema](graphql/dutchie-schema.graphql)
- [Postman Collection](collections/dutchie.postman_collection.json)
- [Open Collection](collections/dutchie.opencollection.json)

### Dutchie Plus Checkout API

The stateful cart and order lifecycle via GraphQL mutations - `createCheckout`, `addItem`, `updateQuantity`, `removeItem`, and `updateCheckout`, plus the `checkout(id)` query. A Checkout tracks its Items and returns a `redirectUrl` used to complete the compliant order. *(Confirmed.)*

- **Human URL:** [https://plus.dutchie.com/plus/docs](https://plus.dutchie.com/plus/docs)
- **Base URL:** `https://plus.dutchie.com/plus/2021-07/graphql`

#### Tags

- Checkout
- Cart
- Orders
- Compliance
- GraphQL

#### Properties

- [Documentation](https://plus.dutchie.com/plus/docs)
- [GraphQL Guide](graphql/dutchie-graphql.md)
- [GraphQL Schema](graphql/dutchie-schema.graphql)
- [Postman Collection](collections/dutchie.postman_collection.json)
- [Open Collection](collections/dutchie.opencollection.json)

## Common Properties

- [GitHub Organization](https://github.com/GetDutchie)
- [LinkedIn](https://www.linkedin.com/company/dutchie)
- [Website](https://dutchie.com)
- [Documentation](https://plus.dutchie.com/plus/docs)
- [Plans](plans/dutchie-plans-pricing.yml)
- [Rate Limits](rate-limits/dutchie-rate-limits.yml)
- [Fin Ops](finops/dutchie-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
