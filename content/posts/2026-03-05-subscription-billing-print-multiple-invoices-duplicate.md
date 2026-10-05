---
title: "Subscription Billing Print Multiple Invoices Duplicate"
date: 2026-03-05T09:00:00+01:00
draft: false
slug: "subscription-billing-print-multiple-invoices-duplicate"
tags: ["al", "business-central", "printing", "problem", "subscriptionbilling"]
description: "Have you run into batch processing failures in Subscription Billing?"
---

Trying to print multiple posted sales invoices from a subscription contract at once? BC throws a duplicate record error and nothing prints.

This is a confirmed bug in the Subscription Billing module, reported on the BCApps GitHub repo. The issue reproduces whenever a user selects more than one posted sales invoice generated from a subscription contract and runs a batch print.

Here's what's happening under the hood. When the print process runs, BC builds a billing details buffer to collect the data for each invoice. The problem is that the `Sub. Contract Billing Details` buffer is being populated without a uniqueness check across multiple invoices in the same run. When two invoices share related contract billing entries, the buffer ends up with duplicate records, and BC throws an error before a single invoice prints.

The worst part is that the error message doesn't tell you which invoices caused the conflict. You select ten invoices, hit print, and the whole job fails. Your users end up printing one invoice at a time as a workaround.

Until a fix ships, the practical workaround is to print subscription contract invoices individually rather than in batch. It's a slower workflow but it avoids the error.

If you're maintaining or customizing the Subscription Billing module, look at how your buffer tables handle multi-record batch operations. A missing uniqueness guard in a buffer is one of the most common sources of this category of error.

Have you run into batch processing failures in Subscription Billing?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open Business Central with the Subscription Billing module
> 2. Navigate to Posted Sales Invoices from a subscription contract
> 3. Select multiple invoices and trigger the print action
> 4. Capture the duplicate record error message
> 5. Annotate the error toast or dialog with a box or arrow

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Bug: Printing multiple posted sales invoices from subscription contracts fails with duplicate record error](https://github.com/microsoft/BCApps/issues/6973)
