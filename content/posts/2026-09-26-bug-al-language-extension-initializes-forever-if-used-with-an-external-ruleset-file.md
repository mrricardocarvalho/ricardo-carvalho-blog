---
title: "[Bug] AL Language Extension initializes forever if used with an external ruleset file"
date: 2026-09-26T09:00:00+01:00
draft: false
slug: "bug-al-language-extension-initializes-forever-if-used-with-an-external-ruleset-file"
tags: ["business-central", "codeanalysis", "problem"]
description: "Have you run into a project that never gets past Preparing project? What turned out to be the cause?"
---

Your AL Language extension is not slow to start. It is never going to start, and your external ruleset file is the reason.

The symptom points everywhere except the real cause. The extension sits in initializing and never becomes ready. No IntelliSense, no symbols. So you check the sandbox, the network, the extension version. All fine. This exact behavior is reported on the microsoft/AL repo: the extension stays stuck at Preparing project, with an external ruleset referenced by al.ruleSetPath whose file includes another ruleset through an HTTPS URL. And it reproduces both with a .code-workspace file and by opening the app folder directly.

The check takes one minute. Temporarily remove al.ruleSetPath and run Developer: Reload Window. If the project loads, you have a useful diagnostic clue. Restore the setting afterwards: removing the ruleset also removes the analysis rules your team relies on. Re-adding it once to confirm the hang returns is an optional test, not a requirement.

Check your extension version before you conclude anything. Users in the issue confirmed that v18.0.2732683 resolves the reported hang. If you still see it on that version or later, do not assume it has the same cause without checking.

Code analysis is nice. An editor that starts is nicer.

Have you run into a project that never gets past Preparing project? What turned out to be the cause?

## The exact code

```json
"al.ruleSetPath": "./.vscode/any.ruleset.json"
```

```json
"includedRuleSets": [
    { "path": "https://any.valid.url/al-rulesets/any.ruleset.json", "action": "Default" }
]
```

> Repro steps for your own environment:
>
> Visual Note (author notes — do NOT paste this block into an image generator):
>
> Exact Code Snippet:
>
> And the referenced ruleset file chaining another ruleset by URL:
>

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [AL Language Extension initializes forever if used with an external ruleset file, microsoft/AL issue 8327](https://github.com/microsoft/AL/issues/8327)
