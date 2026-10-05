---
title: "Bug Quality Management Default Inspection Creation Option To Use Existing Open I"
date: 2026-03-09T09:00:00+01:00
draft: false
slug: "bug-quality-management-default-inspection-creation-option-to-use-existing-open-i"
tags: ["business-central", "problem", "qualitymanagement"]
description: "Have you run into this default setting before? How do you handle it?"
---

The "Inspection Creation Option" in Quality Management can create duplicate inspections if you forget one setting.

By default, it's set to "Always create a new inspection". This means every time you post a receipt, BC happily spawns a new inspection document. Even if one already exists.

A client of mine had hundreds of duplicate inspections piling up. They thought the system was broken. It wasn't. The default setting was just... unhelpful.

The fix? Change the "Inspection Creation Option" to "Use existing open inspection if available". This prevents duplicates and keeps things clean.

You can find this setting in the "Quality Management Setup" page. 

Have you run into this default setting before? How do you handle it?
> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open Business Central and navigate to "Quality Management Setup".
> 2. Locate the "Inspection Creation Option" dropdown.
> 3. Capture a screenshot showing the dropdown with "Use existing open inspection if available" selected.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
