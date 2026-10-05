---
title: "Usage Based Billing Unit Price Ignored"
date: 2026-03-05T09:00:00+01:00
draft: false
slug: "usage-based-billing-unit-price-ignored"
tags: ["al", "business-central", "problem", "subscriptionbilling", "usagebasedbilling"]
description: "Using Usage-Based Billing in BC's Subscription Billing module? Unit prices in your import file are being silently ignored. Only total amounts are proc"
---

Using Usage-Based Billing in BC's Subscription Billing module? Unit prices in your import file are being silently ignored. Only total amounts are processed. 💡

When you import usage data, BC currently reads the total amount per line and disregards any unit price columns. If your usage data provider sends itemized unit prices, they won't flow through. BC treats the total as authoritative.

This is one of four tracked bugs in the Usage-Based Billing area, all documented in a single issue on the BCApps repo.

Workaround for now: pre-calculate total amounts in your import file rather than relying on unit price times quantity. Confirm what BC is actually storing by checking the usage data entries after import.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Bug: Multiple Issues with Usage-Based Billing — unit prices ignored on import](https://github.com/microsoft/BCApps/issues/6972)
