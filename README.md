# Dutchie (dutchie)

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
