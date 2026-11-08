---
title: "Tests run from VS Code Test Explorer / altool runtests crash with NullReferenceException in NavClientHandle.Dispose after Camera.IsAvailable() (Item Card, Customer Card) – pass in AL Test Tool"
date: 2026-10-21T09:00:00+01:00
draft: false
slug: "tests-run-from-vs-code-test-explorer-altool-runtests-crash-with-nullreferenceexception-in"
tags: ["altesting", "business-central", "problem"]
description: "Have you reproduced this runner split with your card-page tests?"
---

A failing Test Explorer run is not proof that your AL test is broken.

GitHub issue #8343 reports tests that pass in AL Test Tool, page 130451, but crash through VS Code Test Explorer or `altool runtests`.

The exception is `System.NullReferenceException` in `NavClientHandle.Dispose`.

The trigger is `Camera.IsAvailable()`.

Opening an Item Card or Customer Card as a TestPage reaches that call through the picture FactBox's `OnOpenPage`.

So a test that never mentions a camera can still hit it.

The report's analysis points to `GuiAllowed()` returning true in test sessions.

The camera path then reaches a client-side DotNet object.

Disposing that object without an attached client appears to be the failure point, not an assertion in the test.

Confirm it with the issue's four-test repro on the documented BC 28.5 container.

Run it through the developer tools, then through page 130451.

Payment Terms passes in both.
The direct camera call, Item Card and Customer Card fail through the developer tools but pass in AL Test Tool.

There is no confirmed fix in the supplied report.

The practical mitigation is to run affected tests in AL Test Tool while investigating the runner failure.

Do not treat that as repaired automation.

And do not assume `OnIsCameraAvailable` can intercept it.
The report says that event runs after the DotNet call.

Have you reproduced this runner split with your card-page tests?

## The exact code

```al
    [Test]
    procedure "02_CameraIsAvailableWithoutAnyPage"()
    var
        Camera: Codeunit Camera;
    begin
        if Camera.IsAvailable() then;
    end;
```

```text
   altool runtests 50100 --server https://<container> --serverinstance BC --port 7049 --tenant default --environmenttype OnPrem --authentication UserPassword --company "CRONUS International Ltd."
```


---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [Microsoft AL issue #8343: camera-related disposal crash in developer-tool test runs](https://github.com/microsoft/AL/issues/8343)
