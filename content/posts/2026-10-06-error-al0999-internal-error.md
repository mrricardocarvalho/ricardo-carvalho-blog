---
title: "error AL0999: Internal Error"
date: 2026-10-06T09:00:00+01:00
draft: false
slug: "error-al0999-internal-error"
tags: ["alcompiler", "business-central", "problem"]
description: "Have you hit AL0999 yet? Did the linked file have anything to do with the real problem?"
---

The painful part of AL0999 is not the crash. It is that VS Code links the error to app.json while the real clue sits in a stack trace most people never open.

AL0999, Internal error, does not mean your AL code is wrong where it points. It means the compiler crashed.

The documented case in the microsoft/AL repo: a full ISV app, minus the system objects above 2000000000 that live in System.app, failing on packaging, publishing, alc.exe from the command line, and the VS Code Problems pane.

The Problems pane linked it to app.json. Nothing else. That is the tell.

When the compiler dies mid-analysis, you never get the real diagnostics. The stack trace is the only useful output.

Turns out the trace is readable. A System.AggregateException wrapping a System.NullReferenceException at SourceControlSymbol.CheckControl(), reached through the SourceRequestPageTypeSymbol and SourceReportTypeSymbol frames.

Read those names. The compiler died while completing a control on a request page inside a report object. Not in app.json.

So the diagnosis path: compile from the command line with alc.exe, capture the full trace, read the symbol types. They tell you which object kind choked the compiler. Here, report request pages and their controls.

The issue documents no confirmed fix. If this were my app, I would isolate report request page controls until the crash reproduces on one object, then take that minimal case to the GitHub thread.

Have you hit AL0999 yet? Did the linked file have anything to do with the real problem?

## The exact code

```text
error AL0999: Internal error: System.AggregateException: One or more errors occurred. ---> System.NullReferenceException: Object reference not set to an instance of an object.
   at Microsoft.Dynamics.Nav.CodeAnalysis.Symbols.SourceControlSymbol.CheckControl() in F:\a\435\s\source\Prod\Microsoft.Dynamics.Nav.CodeAnalysis\Symbols\Source\SourceControlSymbol.cs:line 381
   at Microsoft.Dynamics.Nav.CodeAnalysis.Symbols.SourceRequestPageTypeSymbol.ForceComplete(SourceLocation locationOpt, CancellationToken cancellationToken) in F:\a\435\s\source\Prod\Microsoft.Dynamics.Nav.CodeAnalysis\Symbols\Source\SourceRequestPageTypeSymbol.cs:line 53
   at Microsoft.Dynamics.Nav.CodeAnalysis.Symbols.SourceReportTypeSymbol.ForceComplete(SourceLocation locationOpt, CancellationToken cancellationToken) in F:\a\435\s\source\Prod\Microsoft.Dynamics.Nav.CodeAnalysis\Symbols\Source\SourceReportTypeSymbol.cs:line 56
```


---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [error AL0999: Internal Error, microsoft/AL issue #5036](https://github.com/microsoft/AL/issues/5036)
