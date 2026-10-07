<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset=".github/assets/hero-dark.png">
    <img src=".github/assets/hero.png" alt="pay.me.at landing page" width="880">
  </picture>
</p>

# pay.me.at

Licence keys that keep working when billing goes down.

pay.me.at is one billing rail for a fleet of small, self-hosted products: hosted checkout, signed licence keys, verified webhook fulfillment, and an entitlements API. You bring your own Stripe account, so the money goes straight to the seller and no card data ever touches this service. Every licence is signed and checked offline against a published key set, so a customer's copy keeps running even if this service is down. The rail is built and tested; checkout stays switched off until refund terms, tax handling and terms of service are signed off.

## Features

- **Licence authority with published keys**: licences are signed with a keypair whose public half is served at a standard JWKS endpoint, with key rotation planned so old licences keep verifying.
- **Offline verification**: a product checks its licence against the published keys with no network call, plus a grace period after expiry.
- **Revocation with a defined fallback**: a revocation list is published alongside the keys, with a written rule for what a product does when it cannot fetch it.
- **Verified, idempotent fulfillment**: webhook verification fails closed, and licences are issued only from a verified provider webhook, deduplicated on the event id and on the purchase itself.
- **Plan catalog generated from each product**: the sellable catalog is built from each product's own manifest, so it cannot list a plan the product does not declare.
- **Checkout guards**: a checkout will not start if the billing interval shown differs from the one the provider would charge, or if the tax setting does not resolve.
- **Buyer data redaction**: buyer details are redacted before storage, and the redaction can be replayed over existing rows.
- **No card data, ever**: Stripe-hosted Checkout and Billing Portal only; a mock driver runs a demo mode that charges nobody when no keys are set.

## Screenshots

<table>
  <tr>
    <td width="50%"><picture><source media="(prefers-color-scheme: dark)" srcset=".github/assets/pricing-dark.png"><img src=".github/assets/pricing.png" alt="Pricing"></picture><br><sub>Pricing: the plan catalog generated from each product, shown here in demo mode.</sub></td>
  </tr>
</table>

## Built with

- Next.js 16 (App Router), React 19, TypeScript
- Tailwind CSS 4
- Drizzle ORM + Postgres
- Better Auth
- oRPC
- Stripe (bring your own account), signed licence keys served over JWKS

## Part of the me.at family

pay.me.at is one of my [`*.me.at`](https://me.at) apps. They share one design system, account, and app shell. Development happens in a private monorepo; this repository is the project's public-facing home.

## License

See [LICENSE](LICENSE).
