---
title: "Subscription Billing Missing Global Dimensions"
date: 2026-03-05T09:00:00+01:00
draft: false
slug: "subscription-billing-missing-global-dimensions"
tags: ["al", "business-central", "dimensions", "problem", "subscriptionbilling"]
description: "Did you already work around this in your Subscription Billing setup? 🤔"
---

Did you know you can't edit Global Dimension fields directly on Subscription Billing contract lines? Unlike every other document in BC, they're missing. 🔍

In standard BC documents (Sales Orders, Purchase Orders, Sales Quotes), Global Dimension 1 Code and Global Dimension 2 Code are editable directly on the lines. You can assign dimensions per line without opening the Dimensions window.

On Subscription Billing contract and subscription lines, those fields are absent. You have to open the full Dimensions window every time you want to set line-level dimensions. That's extra clicks on every line, every contract.

There's a second problem compounding this. The Dimensions window title for Subscription Lines is unclear. When you open it from a subscription line, the context in the title bar doesn't reflect which entity (contract line or subscription line) you're editing. That creates confusion on screen-sharing calls and when training new users.

Both issues are tracked as a bug on the BCApps repo and a fix PR is already open.

If you're building extensions on top of the Subscription Billing module or creating training documentation, be aware of this gap. Your users will expect the same dimension editing UX they know from standard BC pages. Warn them in advance if you're implementing subscription workflows, or add the fields yourself in an extension while the fix makes its way in.

Did you already work around this in your Subscription Billing setup? 🤔

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open Business Central and navigate to a Subscription Contract
> 2. Open the contract lines
> 3. Show that Global Dimension 1 and 2 fields are absent on the lines
> 4. Compare side-by-side with a standard Sales Order that shows those fields
> 5. Annotate the missing columns with a red box or arrow

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Bug: Missing Global Dimension fields on contract/subscription lines](https://github.com/microsoft/BCApps/issues/6323)
- [Fix PR: Enhance dimension handling on subscription lines](https://github.com/microsoft/BCApps/pull/6968)
