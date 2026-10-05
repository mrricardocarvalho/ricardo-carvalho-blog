---
title: "Bug Subscriptionbilling Missing Global Dimension Fields On Contract Subscription"
date: 2026-03-06T09:00:00+01:00
draft: false
slug: "bug-subscriptionbilling-missing-global-dimension-fields-on-contract-subscription"
tags: ["business-central", "problem", "subscriptionbilling"]
description: "Bug Subscriptionbilling Missing Global Dimension Fields On Contract Subscription"
---

The “Dimensions” window on Subscription Lines is as unhelpful as it gets. 

It doesn’t show Global Dimension 1 or 2, and good luck figuring that out without a debugger or documentation. 

I ran into this while debugging a subscription billing setup for a client. They were using Global Dimensions to track department and region. But whenever they created a subscription line, those fields weren’t available for selection in the Dimensions window. 

Turns out the “Dimensions” window for subscription lines isn’t using the same logic as sales lines. It’s tied to the Dimension Set ID, not Global Dimension fields. 

The fix? You need to create a custom page extension for the window to pull in Global Dimension 1 and 2 explicitly. Add the fields manually, map them to the subscription line’s Dimension Set ID, and test it thoroughly. 

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open VS Code with the AL project containing the page extension for the Dimensions window.
> 2. Capture the AL code where Global Dimension 1 and 2 are added to the page extension.
> 3. Highlight the lines that map the dimensions to the Dimension Set ID.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
