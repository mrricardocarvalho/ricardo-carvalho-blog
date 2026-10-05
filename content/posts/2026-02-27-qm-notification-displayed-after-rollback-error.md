---
title: "Qm Notification Displayed After Rollback Error"
date: 2026-02-27T09:00:00+01:00
draft: false
slug: "qm-notification-displayed-after-rollback-error"
tags: ["al", "business-central", "notifications", "problem", "qualitymanagement"]
description: "Have you seen phantom notifications in your QM workflows?"
---

Your Quality Inspection notification fired. But the inspection record was rolled back due to an error. Now your users think an inspection exists that doesn't.

This is a confirmed bug in Business Central's Quality Management module, reported on the BCApps GitHub repo.

Here's what happens. When a Quality Inspection record is created, BC fires a notification to the vendor. But if the creation fails downstream and the transaction is rolled back, the notification has already been sent. The user sees a confirmation. The vendor sees a notification. The inspection record doesn't exist.

The root cause is that the notification logic sits outside the transactional boundary. It executes before the full insert is committed, so a rollback doesn't undo the notification.

This is actually part of a broader pattern in the QM module. A related issue was also reported where Commit() runs before posting without proper rollback on failure. Same underlying problem: side effects happening before the transaction is safe.

If you run quality inspections in BC, check whether your notification subscribers respect the transaction boundary. You can guard against it by moving notification logic to OnAfterInsert or wrapping the notification call inside a codeunit that runs after the commit confirmation.

A rolled-back record should never generate a live notification.

Have you seen phantom notifications in your QM workflows?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open VS Code with the AL project containing the QM notification subscriber
> 2. Show the event subscriber code where the notification fires
> 3. Highlight the line where the notification is triggered before commit
> 4. Annotate with a box or arrow showing the timing issue

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Bug: QM Notification displayed even if creation was rolled back](https://github.com/microsoft/BCApps/issues/6855)
- [Related: Commit() before posting without rollback on failure](https://github.com/microsoft/BCApps/issues/6435)
