---
title: "Bug Subscriptionbilling Multiple Issues With Usage Based Billing In Subscription"
date: 2026-03-09T09:00:00+01:00
draft: false
slug: "bug-subscriptionbilling-multiple-issues-with-usage-based-billing-in-subscription"
tags: ["business-central", "problem", "subscriptionbilling"]
description: "Have you run into quirks like this in Subscription Billing? How did you solve them?"
---

The usage-based billing feature in Subscription Billing is powerful, but it has quirks most people miss.

For one, it doesn’t handle all usage scenarios out of the box. If your usage records have timestamps, you may run into trouble. The system doesn’t aggregate overlapping usage entries. That means if you’re logging multiple usage entries for the same customer in the same period, you’ll end up with duplicate charges.

We hit this with a client using IoT data for billing. Devices were sending usage logs every hour. The result? Their customers got invoiced for the same service multiple times.

The fix was surprisingly simple: use a pre-aggregation process to merge usage entries before feeding them into Subscription Billing. A tiny AL extension that grouped by customer, service, and period saved the day.

If you’re using usage-based billing, double-check your data pipeline. It’s not just about importing usage. It’s about shaping it for the system to handle properly.

Have you run into quirks like this in Subscription Billing? How did you solve them?
> Repro steps for your own environment:
>
> **Visual Note (manual action — take this screenshot yourself):**
> 1. Open the AL extension in VS Code that performs the pre-aggregation.
> 2. Capture the specific grouping logic in the AL code.
> 3. Highlight the key lines where the grouping is implemented.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
