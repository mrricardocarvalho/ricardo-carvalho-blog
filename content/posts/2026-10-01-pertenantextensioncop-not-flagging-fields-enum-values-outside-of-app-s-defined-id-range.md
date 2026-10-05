---
title: "PerTenantExtensionCop not flagging fields/enum values outside of app's defined id range"
date: 2026-10-01T09:00:00+01:00
draft: false
slug: "pertenantextensioncop-not-flagging-fields-enum-values-outside-of-app-s-defined-id-range"
tags: ["al", "business-central", "quick-tip"]
description: "PerTenantExtensionCop not flagging fields/enum values outside of app's defined id range"
---

Everyone assumes PerTenantExtensionCop covers your ID ranges. It doesn't. Not for fields and enum values.

A field or enum value can fall outside your app's idRanges without being flagged by PerTenantExtensionCop. Reported case: app declared 50100..50149, field ID 60000 published successfully.

Before publishing a PTE, check those IDs against your declared ranges, not just the PTE range.

A clean analyzer result is not proof those IDs belong to your app.
---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [PerTenantExtensionCop not flagging fields/enum values outside of app's defined id range (microsoft/AL #8313)](https://github.com/microsoft/AL/issues/8313)
