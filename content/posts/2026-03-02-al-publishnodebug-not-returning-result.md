---
title: "Al Publishnodebug Not Returning Result"
date: 2026-03-02T09:00:00+01:00
draft: false
slug: "al-publishnodebug-not-returning-result"
tags: ["al", "business-central", "devtools", "extensions", "problem", "vscode"]
description: "Are you automating AL workflows in VS Code beyond the built-in commands?"
---

Most AL developers use the publish command every day. But did you know you can call it programmatically from another VS Code extension and get the result back?

Well, that's the idea. The command vscode.commands.executeCommand('al.publishNoDebug') lets you trigger a publish from code. Extensions, custom tasks, and automation scripts use this to build CI-like workflows directly inside VS Code.

Here's the catch. The command currently doesn't return a result. It resolves the promise, but gives you no indication of whether the publish succeeded or failed. You fire it and hope for the best.

This is a significant gap if you're building automation around the AL extension. Maybe you're chaining publish with a test run. Maybe you're building a custom deployment panel that shows status. Without a return value, you're forced to scrape the Output panel or watch for diagnostics changes to infer the result.

The issue has been reported on the AL GitHub repo. If Microsoft adds a proper return value (success, failure, error details), it unlocks a whole category of AL tooling extensions that can react to publish outcomes reliably.

If you're building VS Code extensions or tasks that interact with the AL compiler, keep an eye on this issue. A proper command API for the AL extension would change how we build developer tooling for Business Central.

Are you automating AL workflows in VS Code beyond the built-in commands?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open VS Code with an AL project
> 2. Open the Command Palette and show the "AL: Publish without Debugging" command
> 3. Show a snippet of extension code calling vscode.commands.executeCommand('al.publishNoDebug')
> 4. Annotate showing the returned promise resolves with undefined

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [vscode.commands.executeCommand('al.publishNoDebug') not returning result?](https://github.com/microsoft/AL/issues/8181)
