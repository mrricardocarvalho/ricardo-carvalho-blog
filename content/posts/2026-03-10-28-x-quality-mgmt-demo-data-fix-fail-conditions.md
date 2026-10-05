---
title: "28 X Quality Mgmt Demo Data Fix Fail Conditions"
date: 2026-03-10T09:00:00+01:00
draft: false
slug: "28-x-quality-mgmt-demo-data-fix-fail-conditions"
tags: ["business-central", "problem", "qualitymanagement"]
description: "Have you hit inconsistencies like this in Microsoft's demo data? How do you work around them?"
---

Demo data is supposed to help us test. Not break our solutions.

In BC 28.x, Quality Management's demo data can fail validation during imports. The issue? Missing setup data for certain conditions.

I hit this while testing an Item Journal import. The system threw an error: "The field 'Test Type' of table 'Quality Test' cannot be empty." But the demo data didn't include any test types. Classic.

The fix is simple but not obvious. You need to manually add test types to the demo data. Go to the "Test Types" page and create at least one record.

This is a reminder: demo data is a starting point, not a complete solution. Always validate it before assuming it will handle edge cases.

Have you hit inconsistencies like this in Microsoft's demo data? How do you work around them?

## The exact code

```al
table 50000 "Quality Test"
{
    fields
    {
        field(1; "Test Type"; Code[20])
        {
            TableRelation = "Test Type";
        }
    }
}

Steps to reach the exact error or screen:
1. Install the Quality Management module with demo data in BC 28.x.
2. Open the "Item Journals" page and try to import a journal entry with Quality Test fields.
3. Observe the error message referencing the missing 'Test Type'.

Capture guidance:
1. Crop to the relevant 5-12 lines in the table definition.
2. Highlight the `TableRelation = "Test Type";` line.
3. Ensure the screenshot shows the missing relation causing the issue.
```

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> Exact Code Snippet:

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
