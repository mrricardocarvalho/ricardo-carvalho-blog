---
title: "Shopify Fulfillment Service Handling Fix"
date: 2026-02-11T09:00:00+01:00
draft: false
slug: "shopify-fulfillment-service-handling-fix"
tags: ["business-central", "ecommerce", "fulfillment", "shopify", "what-s-coming"]
description: "Are you using third-party fulfillment services with the Shopify connector?"
---

If you use the Shopify connector in Business Central, the fulfillment service handling just got a fix in release 28.x.

A new PR on the BCApps repo addresses how BC processes fulfillment services from Shopify. This is relevant if you're using third-party fulfillment providers (3PLs) that integrate through Shopify's fulfillment service API.

What was the problem?

When Shopify orders use a fulfillment service (a third-party warehouse or logistics provider), BC needs to handle those orders differently than self-fulfilled ones. The previous logic had gaps in how it routed fulfillment service orders, which could lead to incorrect warehouse assignments or missed fulfillment requests.

The fix ensures that orders coming through Shopify's fulfillment service path are correctly identified and processed in BC. The fulfillment service metadata from Shopify is now properly mapped to the corresponding BC warehouse and shipping logic.

Why this matters for your integration. If you've been seeing orders from Shopify that land in the wrong location or don't trigger the right fulfillment workflow, this could be your root cause. Teams using 3PL providers through Shopify were most affected.

This is an open PR targeting the 28.x branch, so it should land in an upcoming update. If you're on BC 28 with the Shopify connector, keep your environment updated. And if you've built custom workarounds for fulfillment routing, you may be able to retire them once this ships.

Are you using third-party fulfillment services with the Shopify connector?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open the GitHub PR page for microsoft/BCApps#6959
> 2. Capture the PR description showing the fulfillment service changes
> 3. Or show the Shopify connector setup page in BC with fulfillment service configuration
> 4. Annotate the key change or configuration option

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [PR: Fix fulfillment service handling in Shopify connector (28.x)](https://github.com/microsoft/BCApps/pull/6959)
