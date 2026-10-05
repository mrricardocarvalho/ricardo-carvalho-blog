---
title: "Master Released Contract Deferral Shows Wrong Sign For Vendor Subscription Contr"
date: 2026-03-06T09:00:00+01:00
draft: false
slug: "master-released-contract-deferral-shows-wrong-sign-for-vendor-subscription-contr"
tags: ["business-central", "deferral", "what-s-coming"]
description: "Have you hit this in your environment yet? How are you working around it?"
---

The Contract Deferral feature has a bug in BC. Vendor subscription contracts show reversed signs after release.

Microsoft confirmed this issue in recent builds. It flips the deferred amounts for vendor contracts, causing negative values where positives should be.

Why does this matter? If you're using Contract Deferral for vendor subscriptions, your financial reporting is off. This bug affects both manual and auto-posted deferrals.

The fix is coming in the next cumulative update. Until then, check your vendor deferral entries manually or disable automation for these contracts.

Have you hit this in your environment yet? How are you working around it?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open BC with a vendor subscription contract using Contract Deferral.
> 2. Navigate to the deferral entries page.
> 3. Capture the entries showing reversed signs.
> 4. Annotate the incorrect values with a box or arrow.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
