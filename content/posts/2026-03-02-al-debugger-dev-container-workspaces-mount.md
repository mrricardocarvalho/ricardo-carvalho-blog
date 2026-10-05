---
title: "Al Debugger Dev Container Workspaces Mount"
date: 2026-03-02T09:00:00+01:00
draft: false
slug: "al-debugger-dev-container-workspaces-mount"
tags: ["al", "business-central", "debugging", "devcontainers", "docker", "problem"]
description: "Have you hit path resolution issues with the AL debugger in containers?"
---

Using Dev Containers for AL development? Your debugger might silently fail to open source files when it hits a breakpoint.

There's an open issue on the AL GitHub repo affecting developers who use the default /workspaces mount path in Dev Containers. The AL debugger hits the breakpoint, pauses execution, but can't resolve the file path to show you the source code. You're staring at a call stack with no code to read.

The problem is a path mismatch. When you create a Dev Container with the default configuration, VS Code mounts your workspace under /workspaces/your-project. But the AL debugger resolves source file paths relative to a different root. The paths don't align, so the debugger knows where it stopped but can't map that location back to an actual file in your editor.

This is particularly frustrating because everything else works. IntelliSense runs fine. Publishing works. The app deploys and executes. It's only when you need to step through code that the debugger breaks down silently.

The workaround reported by developers is to customize your devcontainer.json to explicitly set the workspace mount path to match what the AL debugger expects. Alternatively, you can configure the launch.json with explicit path mappings using the "breakOnNext" and source path settings.

If you're setting up AL Dev Containers, test your debugger before you invest hours in the development workflow. A broken debugger in a containerized setup defeats the purpose of the whole environment.

Have you hit path resolution issues with the AL debugger in containers?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open VS Code with a Dev Container running an AL project
> 2. Show the debugger paused on a breakpoint with the "Could not open file" or empty editor state
> 3. Capture the call stack panel showing the file path that can't be resolved
> 4. Annotate the path mismatch between the expected and actual mount paths

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [AL Debugger Cannot Open Files in Dev Container with Default /workspaces Mount](https://github.com/microsoft/AL/issues/8153)
