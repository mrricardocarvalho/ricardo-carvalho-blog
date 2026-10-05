---
title: "Blob Field Upload Onvalidate Bypass"
date: 2026-03-03T09:00:00+01:00
draft: false
slug: "blob-field-upload-onvalidate-bypass"
tags: ["al", "blob", "business-central", "problem", "validation"]
description: "Were you relying on OnValidate for Blob field uploads? 🤔"
---

Did you know that uploading a file to a Blob field in Business Central can silently skip your OnValidate trigger? 🔍

There's an open issue on the AL GitHub repo that exposes a subtle behavior. When a user uploads a file into a Blob field through the standard UI action, the OnValidate trigger on that field doesn't fire. Your validation logic never runs.

This matters if you're relying on OnValidate to enforce rules on uploaded content. Maybe you check file size. Maybe you validate the file extension. Maybe you write an audit log entry when a document is attached. None of that executes during upload.

The reason is that the file upload mechanism writes directly to the Blob field without going through the normal field assignment path. It bypasses the validate logic entirely.

If you need to enforce rules on Blob field content, subscribe to OnAfterModifyRecord or use a separate action that wraps the upload with your validation logic. Don't rely on the field-level OnValidate for Blob types.

This is one of those edge cases that only surfaces in production when someone uploads a file that should have been rejected.

Were you relying on OnValidate for Blob field uploads? 🤔

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open VS Code with an AL project that has a Blob field with OnValidate trigger
> 2. Show the trigger code that should fire on upload
> 3. Set a breakpoint and demonstrate it doesn't hit when uploading a file
> 4. Annotate showing the bypassed validation path

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Bug: Blob field upload and OnValidate](https://github.com/microsoft/AL/issues/8145)
