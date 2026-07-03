# Dutchie Plus GraphQL API

Dutchie Plus is Dutchie's headless cannabis-commerce API. It lets developers build
fully custom, branded dispensary storefronts (typically Next.js, Astro, or Gatsby)
against Dutchie's ecommerce backend: query a retailer's live menu, products,
variants, potency, and specials, then drive a stateful, compliance-aware
cart/checkout that ends in a completed order.

- **Endpoint:** `https://plus.dutchie.com/plus/2021-07/graphql`
- **Transport:** GraphQL over HTTPS `POST`
- **Auth:** `Authorization: Bearer <retailer API key>` (the key scopes requests to a retailer)
- **Playground:** `https://plus.dutchie.com/plus/2021-07/graphql`
- **Documentation:** https://plus.dutchie.com/plus/docs
- **Reference example:** [GetDutchie/dutchie-plus-nextjs-example](https://github.com/GetDutchie/dutchie-plus-nextjs-example)
- **Schema (SDL):** [dutchie-schema.graphql](dutchie-schema.graphql)

> **Note:** Dutchie has announced a 2026 sunset/deprecation of the Plus headless
> commerce API. Confirm availability with Dutchie before building against it.

Operations below are marked **[CONFIRMED]** when they appear verbatim in the
official Dutchie Plus Next.js example, or **[MODELED]** when they are referenced in
Dutchie Plus documentation / the 2021-07 schema but not exercised by that example.

## Making a request

Every call is an HTTP `POST` of a JSON body `{ "query": "...", "variables": {...} }`.

```bash
curl -X POST https://plus.dutchie.com/plus/2021-07/graphql \
  -H "Authorization: Bearer $DUTCHIE_PLUS_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query":"query Menu($category: Category) { menu(filter: { category: $category }, pagination: { limit: 12, offset: 0 }) { products { id name } } }","variables":{"category":"FLOWER"}}'
```

## Menu & Products  [CONFIRMED]

The core storefront query. `menu(filter, pagination)` returns a page of `Product`
records for the scoped retailer.

```graphql
query Menu($category: Category) {
  menu(filter: { category: $category }, pagination: { limit: 12, offset: 0 }) {
    products {
      id
      name
      description
      image
      category
      strainType
      brand { name }
      potencyThc { formatted }
      potencyCbd { formatted }
      variants {
        option
        priceRec
        priceMed
        specialPriceRec
        specialPriceMed
      }
    }
  }
}
```

A smaller "home page" variant simply lowers the pagination limit:

```graphql
query HomePageMenu($category: Category) {
  menu(filter: { category: $category }, pagination: { limit: 6, offset: 0 }) {
    products { id name image variants { option priceRec } }
  }
}
```

## Retailers / Dispensaries  [MODELED]

List the dispensaries connected to your account and inspect one retailer's
metadata, address, hours, and supported order/pricing types. The active retailer
scope is established by the API key.

```graphql
query Retailers {
  retailers {
    id
    name
    slug
    status
    offerDelivery
    offerAnyPickup
    pricingTypes
    address { line1 city state postalCode }
    hours { day startTime endTime orderType }
  }
}
```

## Specials / Deals  [MODELED]

List a retailer's active promotions. The discounts these represent surface on the
menu as `specialPriceRec` / `specialPriceMed` on each product variant (those
special-price fields are **[CONFIRMED]** on the `Variant` type).

```graphql
query Specials {
  specials {
    id
    name
    description
    type
    startDate
    endDate
  }
}
```

## Cart & Checkout  [CONFIRMED]

Checkout is a stateful object built up with mutations. Create a checkout, add
product variants, adjust quantities, and read a `redirectUrl` used to complete the
compliant order. The `Checkout` fragment used throughout the example is:

```graphql
fragment Checkout on Checkout {
  id
  orderType
  pricingType
  redirectUrl
  items {
    id
    option
    quantity
    product {
      name
      image
      brand { name }
      variants { option priceRec }
    }
  }
}
```

### Create a checkout

```graphql
mutation CreateCheckout($orderType: OrderType!, $pricingType: PricingType!) {
  createCheckout(orderType: $orderType, pricingType: $pricingType) {
    ...Checkout
  }
}
```

Variables:

```json
{ "orderType": "DELIVERY", "pricingType": "RECREATIONAL" }
```

### Add an item

```graphql
mutation AddItemToCheckout(
  $checkoutId: ID!
  $productId: ID!
  $quantity: Int!
  $option: String!
) {
  addItem(
    checkoutId: $checkoutId
    productId: $productId
    quantity: $quantity
    option: $option
  ) {
    ...Checkout
  }
}
```

### Update an item quantity

```graphql
mutation UpdateCheckoutItemQuantity(
  $checkoutId: ID!
  $itemId: ID!
  $quantity: Int!
) {
  updateQuantity(checkoutId: $checkoutId, itemId: $itemId, quantity: $quantity) {
    ...Checkout
  }
}
```

### Remove an item

```graphql
mutation RemoveItemFromCheckout($checkoutId: ID!, $itemId: ID!) {
  removeItem(checkoutId: $checkoutId, itemId: $itemId) {
    ...Checkout
  }
}
```

### Change order type / pricing type

```graphql
mutation UpdateCheckout(
  $checkoutId: ID!
  $orderType: OrderType!
  $pricingType: PricingType!
) {
  updateCheckout(
    checkoutId: $checkoutId
    orderType: $orderType
    pricingType: $pricingType
  ) {
    ...Checkout
  }
}
```

### Fetch an existing checkout

```graphql
query Checkout($id: ID!) {
  checkout(id: $id) {
    ...Checkout
  }
}
```

## Enums

- **Category** `[CONFIRMED]`: `FLOWER`, `VAPORIZERS`, `CONCENTRATES`, `EDIBLES`,
  `TINCTURES`, `TOPICALS`, `ACCESSORIES`, `APPAREL`, `CBD`, `CLONES`, `PRE_ROLLS`,
  `SEEDS`, `NOT_APPLICABLE`
- **StrainType** `[CONFIRMED]`: `SATIVA`, `HYBRID`, `INDICA`, `HIGH_CBD`
- **OrderType** `[CONFIRMED]`: `PICKUP`, `DELIVERY`
- **PricingType** `[CONFIRMED]`: `RECREATIONAL`, `MEDICAL`

## Subscriptions / WebSockets

Dutchie Plus does **not** document a public GraphQL subscription or WebSocket
transport. All operations are request/response GraphQL queries and mutations over
HTTPS. See [../review.yml](../review.yml).
