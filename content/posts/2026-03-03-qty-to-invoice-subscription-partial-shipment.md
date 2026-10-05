---
title: "Qty To Invoice Subscription Partial Shipment"
date: 2026-03-03T09:00:00+01:00
draft: false
slug: "qty-to-invoice-subscription-partial-shipment"
tags: ["al", "business-central", "invoicing", "problem", "subscriptionbilling"]
description: "Have you run into quantity mismatches on subscription billing lines?"
---

You shipped half an order with subscription items, and now BC won't let you invoice the rest. The "Qty. to Invoice" field has a wrong value and posting fails.

This is a confirmed bug in the Subscription Billing module, tracked on the BCApps GitHub repo. After a partial shipment of subscription items, Business Central incorrectly sets "Qty. to Invoice" to a non-zero value on lines that shouldn't be invoiceable yet.

Here's the scenario. You have a sales order with subscription items. You do a partial shipment. Then you try to post the invoice for what you actually shipped. BC throws a posting error because it calculated the invoiceable quantity wrong on the remaining subscription lines.

The root cause is in how the Subscription Billing extension handles the quantity split between shipped and unshipped lines. When a partial shipment is posted, the logic that recalculates "Qty. to Invoice" on the remaining lines doesn't properly account for the subscription item type. It treats them like regular inventory items, leaving a non-zero invoiceable quantity where it should be zero.

A fix PR is already open on the BCApps repo. Until it lands, you can work around it by manually resetting the "Qty. to Invoice" field on the affected lines before posting the invoice. Or you can post shipment and invoice separately, adjusting the quantities on each step.

If you use subscription items with partial shipments, check your open orders for incorrect "Qty. to Invoice" values. One wrong line can block the entire invoice posting.

Have you run into quantity mismatches on subscription billing lines?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open Business Central and navigate to a Sales Order with subscription items
> 2. Show the Sales Lines with the incorrect "Qty. to Invoice" value highlighted
> 3. Capture the posting error that results from the wrong quantity
> 4. Annotate the "Qty. to Invoice" field with a box or arrow

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Bug: "Qty. to Invoice" incorrectly set for subscription items after partial shipment](https://github.com/microsoft/BCApps/issues/6319)
- [Fix PR: Subscription Billing partial shipment quantity correction](https://github.com/microsoft/BCApps/pull/6918)
