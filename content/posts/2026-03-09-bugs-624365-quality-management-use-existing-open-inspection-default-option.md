---
title: "Bugs 624365 Quality Management Use Existing Open Inspection Default Option"
date: 2026-03-09T09:00:00+01:00
draft: false
slug: "bugs-624365-quality-management-use-existing-open-inspection-default-option"
tags: ["business-central", "problem", "qualitymanagement"]
description: "Have you encountered this? How do you manage quality inspections in custom workflows?"
---

"Use existing open inspection" in Quality Management doesn't always work as expected.

Here's why: the option assumes that an open inspection exists for the same item and location. If that's not the case, BC skips the check and creates a new one. 

A client was puzzled why multiple inspections were created for the same item. Turned out, their process didn't always create open inspections where expected, and BC didn't warn them. It just created duplicates.

The fix? Force BC to validate open inspections before creating a new one. Add a custom check in the codeunit processing the quality order creation.

```al
if not QualityOrderExists(ItemNo, LocationCode) then
    Error('No open inspection exists for this item and location.');
```

Don't rely on defaults if your process isn't airtight.

Have you encountered this? How do you manage quality inspections in custom workflows?
> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open the AL project in VS Code with the custom codeunit handling quality order creation.
> 2. Capture the snippet where the custom validation is added.
> 3. Highlight the `QualityOrderExists` function call and the `Error` line with a box or arrow.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
