---
title: "Al Language Server Crashes Invalid Parameter Types"
date: 2026-02-26T09:00:00+01:00
draft: false
slug: "al-language-server-crashes-invalid-parameter-types"
tags: ["al", "business-central", "languageserver", "problem", "vscode"]
description: "Have you ever had the AL Language Server crash on you for a non-obvious reason?"
---

Your AL Language Server keeps crashing and you have no idea why? The culprit might be hiding in your XML documentation comments.

I hit this recently on a mature codebase with hundreds of documented procedures. The Language Server would load, index for a few seconds, then silently die. No error toast. No output log. Just gone.

After isolating extensions one by one (the slowest debugging process known to developers), I narrowed it down to a single file. The procedure had XML doc comments with parameter types that didn't match the actual signature.

Something like this:

```al
/// <summary>
/// Processes the sales document.
/// </summary>
/// <param name="SalesHeader">The sales header record.</param>
/// <param name="PostingDate">The posting date.</param>
procedure ProcessDocument(SalesHeader: Record "Sales Header")
```

Notice the mismatch — the doc comment references a `PostingDate` parameter that doesn't exist in the procedure signature. The Language Server's documentation parser choked on this inconsistency and crashed the entire process.

The fix was straightforward: align the XML doc comments with the actual parameter list. But finding it took hours because the crash gave zero indication of which file or procedure was responsible.

If your Language Server is unstable, search your codebase for `<param name=` and cross-reference against actual procedure signatures. A quick regex can save you an afternoon.

Have you ever had the AL Language Server crash on you for a non-obvious reason?
> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open VS Code with the AL project containing the problematic procedure
> 2. Show the XML documentation comments with the mismatched parameter
> 3. Capture the before (mismatched) and after (fixed) versions side by side
> 4. Highlight the extra/missing parameter line with a box or arrow

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
