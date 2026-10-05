---
title: "al_compile/al_build MCP tools return stale cached success after a cross-project breaking change"
date: 2026-09-30T09:00:00+01:00
draft: false
slug: "al-compile-al-build-mcp-tools-return-stale-cached-success-after-a-cross-project-breaking-c"
tags: ["business-central", "mcp", "problem"]
description: "Have you wired the AL MCP tools into your workflow yet? How do you verify what they tell you?"
---

The MCP tool said the build succeeded. It was replaying a result from before your breaking change.

The AL MCP tools al_compile and al_build cache their compile results. And that cache has a blind spot: when a breaking change lands in one project, the cached success for the project that depends on it is not invalidated. You ask for a compile, the tool replays the last known result, and your code is actually broken. This exact trap is issue 8325 on the microsoft/AL repo.

How do you catch it? Cross-check the two worlds. A genuine command-line compile with alc.exe against the same files correctly fails with AL0132 while the tool keeps answering success. If those two disagree, you are talking to a cache.

And the cache is tied to the running MCP server process. The stale result survives repeated calls, new sessions and even re-registering the project. The only thing that cleared it in the report was a full restart of that process. Until Microsoft ships a fix, that restart is your reset button.

The dangerous part is who reads the answer. These tools exist to feed agents. An agent takes success at face value, keeps going, and marks the task done. Nobody looks at the code again until a real build or deployment exposes it.

So treat every success as provisional. After you touch a dependency, run an independent compile, alc.exe on the command line, and read its errors. That is the verification the issue itself used. And if an agent drives your workflow, make it prove the compile with an independent check before it declares victory.

Have you wired the AL MCP tools into your workflow yet? How do you verify what they tell you?
> Repro steps for your own environment:
>
> Visual Note (manual capture, only if the issue can be reproduced):
>
> Create one composite image from real captures of the same workspace and the same source state.
>
> Left: show the dependent AL project still referencing the old field name:
>     JobTask."MyCustomField" := true;

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [GitHub issue 8325: al_compile/al_build MCP tools return stale cached success after a cross-project breaking change](https://github.com/microsoft/AL/issues/8325)
