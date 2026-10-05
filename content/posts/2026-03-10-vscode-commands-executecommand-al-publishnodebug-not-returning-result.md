---
title: "Vscode Commands Executecommand Al Publishnodebug Not Returning Result"
date: 2026-03-10T09:00:00+01:00
draft: false
slug: "vscode-commands-executecommand-al-publishnodebug-not-returning-result"
tags: ["business-central", "problem", "vscode"]
description: "Would you expect this command to return a result, or do you treat it as fire-and-forget and read diagnostics instead?"
---

`vscode.commands.executeCommand('al.publishNoDebug')` does not return a result. Should it?

This is one of those API design decisions that can make you question your own debugging process. If you’ve used this command in an extension or script, you’ve probably noticed it doesn’t give feedback. No success, no failure. Just silence.

Here’s the context: I was working on a CI/CD pipeline for AL extensions. I wanted to trigger a publish without debugging directly from VS Code. The command worked, but I had no idea if it succeeded or failed unless I checked manually in BC.

Why is it designed this way? Likely because it’s meant to be a fire-and-forget operation. The problem is that you lose visibility into what actually happened. Did the publish succeed? Did it fail? If so, why?

My workaround: I built a wrapper that listens for diagnostic messages and logs them after the command runs. It’s not elegant, but at least I know whether my action had the intended result.

Would you expect this command to return a result, or do you treat it as fire-and-forget and read diagnostics instead?

## The exact code

```ts
const result = await vscode.commands.executeCommand('al.publishNoDebug');
console.log('publish result:', result);
```

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> Exact Code Snippet:
>
>
> Steps to reach the exact error or screen:
> 1. Open a VS Code extension project that calls `vscode.commands.executeCommand('al.publishNoDebug')`.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
