---
title: "Error to consume automation variable Dynamics 365 Business Central"
date: 2026-10-28T09:00:00+01:00
draft: false
slug: "error-to-consume-automation-variable-dynamics-365-business-central"
tags: ["business-central", "dynamicsnav", "problem"]
description: "What evidence do you collect when a legacy integration works only on its first call?"
---

An Automation call that works once and then fails is not automatically an AL migration problem.

A Business Central on-premises question shows this sequence:

EVALUATE(_PC, PCStr);
CREATE(_Export, TRUE, TRUE);
_Export.process(_PC);

The author says the first call works, then an error appears. The question does not supply the exact error text, component identity or BC build.

The accepted answer adds CLEAR(_Export) before CREATE, to clear the Automation variable before creating it again.

That is a reported remedy for this legacy Automation example, not a universal fix for COM errors and not evidence that Automation is an AL data type.

For a comparable legacy case, inspect the variable lifecycle and test the same action twice in the affected environment. Check whether clearing the variable changes the result before investigating component registration or proposing a migration.

Do not substitute a generic cloud migration explanation for the code and execution pattern actually reported.

What evidence do you collect when a legacy integration works only on its first call?

## The exact code

```text
EVALUATE(_PC, PCStr);
CLEAR(_Export);//to clean your automation
CREATE(_Export, TRUE, TRUE);
_Export.process(_PC);
```

> Source: excerpt from the accepted answer linked below; not locally executed.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [Original question and reported first-call behavior](https://stackoverflow.com/questions/60329326/error-to-consume-automation-variable-dynamics-365-business-central)
- [Accepted answer: CLEAR before CREATE](https://stackoverflow.com/a/60329398)
