---
title: "Quality Mgmt Demo Data Fix Fail Conditions"
date: 2026-03-06T09:00:00+01:00
draft: false
slug: "quality-mgmt-demo-data-fix-fail-conditions"
tags: ["business-central", "problem", "qualitymanagement"]
description: "Quality Mgmt Demo Data Fix Fail Conditions"
---

Your test runs fail because of demo data? It's not the test code.

The issue often comes from how demo data violates the actual business rules. Quality Management tables are notorious for this.

Last month, I hit this while testing fail conditions on a Quality Management solution. The demo data was missing required fields like "Test Status" and "Assigned User" in the Quality Order table.

The test failed not because of the AL code, but because the data setup was invalid. Demo data doesn't respect constraints like mandatory fields or key relationships.

Solution: Before running tests, validate your demo data with the same conditions your AL code enforces. For Quality Management, check field requirements in the Quality Order and Quality Test tables.

Have you run into bad demo data breaking your tests? How did you fix it?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open VS Code with the Quality Management project.
> 2. Locate the failing AL test code for Quality Order validation.
> 3. Highlight the key area where demo data caused the failure, especially missing "Test Status" field.
> 4. Annotate the missing fields with a box or arrow.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
