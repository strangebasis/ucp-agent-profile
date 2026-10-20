# ucp-agent-profile

This repository exists to serve one small file, [`ucp-agent-profile.json`](ucp-agent-profile.json). It is the
**agent profile** of a personal hobby project: a private tracker of Gudetama merchandise, kept by a fan for their
own collection. It is not a commercial service, and nobody else uses it.

## Why it is public

Shops built on Shopify offer a catalog API for software agents, based on the
[Universal Commerce Protocol](https://ucp.dev) (UCP). Each call names a profile URL, so the shop can see who is
asking and what the caller may do. The shop fetches the profile from a public address, and this is that address:

    https://cdn.jsdelivr.net/gh/strangebasis/ucp-agent-profile@v1/ucp-agent-profile.json

That is the [jsDelivr](https://www.jsdelivr.com) CDN serving this repository's `v1` tag. A CDN is used because the
UCP specification requires profiles to be served with a `Cache-Control: public` header, which GitHub Pages cannot
send.

## What the agent does

- Searches a shop's public catalog for "gudetama": about one request a day, plus an ordinary read of a product
  page when a new product appears.
- Declares read-only catalog search and lookup. It never creates a cart or a checkout and never buys anything.
- Says who it is in every request: `User-Agent: getgude-catalog/1.0 (personal hobby project; +` followed by the
  address above and a closing parenthesis.
- Backs off on `429` and honors `Retry-After`. It does not try to get around a refusal.
- Keeps product titles, prices, links and photo links for personal use.

## If you run a shop and would rather not be asked

Open an issue on this repository and the project will stop asking your shop.

## What is in the file

Only protocol metadata: the UCP version and the three capabilities it uses (catalog search, catalog lookup and
Shopify's catalog extension). It holds no personal data.
