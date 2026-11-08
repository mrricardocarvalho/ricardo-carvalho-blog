---
title: "forceUpgrade does not work anymore"
date: 2026-02-12T09:00:00+01:00
draft: false
slug: "forceupgrade-does-not-work-anymore"
tags: ["al", "business-central", "problem"]
description: "Did you also write off forceUpgrade? How do you verify your upgrade codeunits ran?"
---

forceUpgrade did not stop working in BC 20. What stopped is your ability to debug it.

A dev reported this on the microsoft/AL repo: publish in dev scope with an unchanged version, an upgrade codeunit with a breakpoint in OnUpgradePerCompany, forceUpgrade true in launch.json. The breakpoint never fires.

Turns out the flag is not the problem. Per Microsoft in the thread: the debugger has to be attached BEFORE the extension is published. A regular F5 publish attaches too late, so the breakpoint in OnUpgradePerCompany never fires. The community explanation goes further: since 2020 release wave 2, upgrade and install codeunits run in internal system sessions that cannot be debugged. If you debugged one years ago, you were riding a bug that got fixed.

The response in the thread was clear: forceUpgrade should still force the run even with an unchanged version, however you publish.

Confirm it yourself:

1. Open the debug window and read the request query parameters. You want ForceUpgrade=true in dev/apps?tenant=default&SchemaUpdateMode=synchronize&ForceUpgrade=true&DependencyPublishingOption=default. If it is there, the flag is sent.

2. Swap the breakpoint for a message and publish. If the message shows, the codeunit ran. Only the debugger was lying.

If you actually need to step through it, the thread has a path: start an attach configuration with a WebServiceClient client type, then run Publish Extension Without Building. It made the 2020 wave 2 changelog and missed the docs. And here is the part Microsoft did not expect: their own dev said it should not work and is not designed that way, yet they were surprised it does. It works on SaaS sandboxes too.

When in doubt, bump the version in app.json. Boring, but it always triggers the upgrade.

Did you also write off forceUpgrade? How do you verify your upgrade codeunits ran?

## The exact code

```al
codeunit 50000 "My Upgrade"
{
    Access = Internal;
    Subtype = Upgrade;

    trigger OnUpgradePerCompany()
    begin
        // Set your breakpoint here, or throw message
    end;
}
```

```json
{
    "forceUpgrade": true
}
```


---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [forceUpgrade does not work anymore (microsoft/AL issue 7037)](https://github.com/microsoft/AL/issues/7037)
