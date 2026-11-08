---
title: "How to Debug Dynamics 365 Business Central ( Wave2 ) in a correct way?"
date: 2026-10-27T09:00:00+01:00
draft: false
slug: "how-to-debug-dynamics-365-business-central-wave2-in-a-correct-way"
tags: ["business-central", "debugging", "quick-tip"]
description: "What do you record first?"
---

Before changing business logic, record your debugging setup.

For Business Central, start with:

- Exact BC version
- Deployment type
- Action being tested
- Debugger configuration
- Breakpoint location
- Expected and observed result

That checklist separates a business failure from a debugging question. It is not a fix for a specific incident.

What do you record first?
---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [Microsoft Learn: Debugging in AL](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-debugging)
