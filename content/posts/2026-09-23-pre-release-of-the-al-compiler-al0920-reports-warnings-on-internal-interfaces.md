---
title: "Pre-release of the AL compiler: AL0920 reports warnings on internal interfaces"
date: 2026-09-23T09:00:00+01:00
draft: false
slug: "pre-release-of-the-al-compiler-al0920-reports-warnings-on-internal-interfaces"
tags: ["alcompiler", "business-central", "what-s-coming"]
description: "Are you building against pre-release compiler versions, or do you wait for stable? And if you are on pre-release, did AL0920 show up for you?"
---

AL0920 warnings just started appearing on internal interfaces with the pre-release AL compiler. Your first instinct is to refactor. Don't.

It is tracked as issue 8279 on the microsoft/AL repo. The report is simple: on a pre-release compiler build, AL0920 warnings appear against internal interfaces.

Why does this matter?

Because the pre-release channel is where the next stable compiler takes shape. If your CI treats warnings as errors, a new diagnostic can break builds that were clean yesterday. And if the warnings are noise rather than signal, you want to know that before you start refactoring interfaces that were fine all along.

How to prepare:

1. On the pre-release channel? Reproduce it and add your details to the issue. Repro information moves compiler reports forward fast.
2. Run pipelines with warnings as errors? Decide now how a new diagnostic code gets handled before it reaches stable.
3. Do not rewrite internal interfaces just to silence a warning. Confirm the behavior first.

The pre-release channel exists for exactly this. Find the rough edges early, report them, and let the stable release arrive boring.

Are you building against pre-release compiler versions, or do you wait for stable? And if you are on pre-release, did AL0920 show up for you?
---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [GitHub issue: Pre-release of the AL compiler: AL0920 reports warnings on internal interfaces](https://github.com/microsoft/AL/issues/8279)
