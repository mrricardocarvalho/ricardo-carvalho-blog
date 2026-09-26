---
title: "'Value is not accepted' / Code analyzer rules not recognized in ruleset file."
date: 2026-09-26T09:00:00+01:00
draft: false
slug: "value-is-not-accepted-code-analyzer-rules-not-recognized-in-ruleset-file"
tags: ["business-central", "codeanalysis", "quick-tip"]
description: "'Value is not accepted' / Code analyzer rules not recognized in ruleset file."
---

"Value is not accepted" in your ruleset.json usually does not mean the rule ID is wrong.

The AL editor fails to recognize some code analyzer rules in the ruleset and flags them anyway. Known issue, tracked on the microsoft/AL repo.

Do not delete the rule over the squiggle. Build first, then check whether the analyzer actually applies it.

Your ruleset stays intact instead of getting gutted over an editor false positive.
---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - ["Value is not accepted" / Code analyzer rules not recognized in ruleset file (microsoft/AL #8338)](https://github.com/microsoft/AL/issues/8338)
