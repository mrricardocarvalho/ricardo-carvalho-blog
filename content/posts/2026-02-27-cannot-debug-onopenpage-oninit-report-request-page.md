---
title: "Cannot Debug Onopenpage Oninit Report Request Page"
date: 2026-02-27T09:00:00+01:00
draft: false
slug: "cannot-debug-onopenpage-oninit-report-request-page"
tags: ["al", "business-central", "debugging", "problem", "reports"]
description: "Can't hit breakpoints on OnOpenPage or OnInit of a Report's request page? You're not alone. This is an open issue on the AL GitHub repo."
---

Can't hit breakpoints on OnOpenPage or OnInit of a Report's request page? You're not alone. This is an open issue on the AL GitHub repo.

The request page triggers fire before the debugger fully attaches to the report execution context. Your breakpoints are set, but the debugger misses them.

Workaround: call the report from AL code using Report.RunModal() instead of launching it from the UI. The debugger attaches earlier when triggered programmatically.

This has been reported to Microsoft and is tracked as an open issue.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Cannot debug OnOpenPage and OnInit of Report's request page](https://github.com/microsoft/AL/issues/8171)
