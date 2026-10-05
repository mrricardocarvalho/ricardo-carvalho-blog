---
title: "Exposing Agentsetupbuffer Copying In Bc 28"
date: 2026-02-26T09:00:00+01:00
draft: false
slug: "exposing-agentsetupbuffer-copying-in-bc-28"
tags: ["agents", "ai", "business-central", "copilot", "what-s-coming"]
description: "Have you started automating your Copilot agent deployments yet?"
---

Business Central 28 just made AI Agent setup programmable — and most developers haven't noticed yet.

Microsoft quietly exposed the copying of the AgentSetupBuffer in release 28.

What does that mean in practice?

Until now, configuring Copilot agents in BC was a manual, UI-driven process. If you wanted to replicate an agent configuration across environments — dev, test, production — you had to redo the setup every single time.

Now, with the AgentSetupBuffer copy functionality exposed, you can programmatically duplicate agent configurations. Think of it as the missing piece for CI/CD pipelines that include AI agents.

This matters because agent adoption is accelerating. Teams that automate their agent deployment will iterate faster than those clicking through setup wizards in every environment.

Here's what I'd do right now:

Pull the latest BC 28 preview. Look at the AgentSetupBuffer table and its new public methods. Start building your agent configuration migration scripts before your next environment refresh catches you off guard.

Have you started automating your Copilot agent deployments yet?
> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open Business Central 28 preview
> 2. Navigate to the AgentSetupBuffer table definition or the Agent Setup page
> 3. Capture the new copy/export functionality
> 4. Annotate the key method or action with a box or arrow

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
