---
title: "Fa Scan Entries Date Not Valid Zero Duration"
date: 2026-03-04T09:00:00+01:00
draft: false
slug: "fa-scan-entries-date-not-valid-zero-duration"
tags: ["al", "business-central", "fixedassets", "problem", "scanning"]
description: "Have you encountered cryptic date validation errors in Fixed Assets?"
---

Running Fixed Asset scanning in Business Central 28 and getting "The date is not valid"? The problem isn't your data. It's a zero-duration field that should never have been empty.

This bug was caught on the BCApps GitHub repo and fix PRs are already open for both 28.0 and 28.x branches. The root cause is in the FA Scan entries logic where the "Last time scanned" field contains a 0D (zero duration) value.

Here's what happens. When you run the FA scanning process, BC tries to calculate the next scan date based on the last scanned timestamp. But if that field was never populated, it holds a 0D value. The date arithmetic chokes on it because you can't add an interval to a zero duration and get a valid date. BC throws "The date is not valid" with no further context.

This is particularly frustrating because the error message gives you no clue about which field caused it. You're looking at your FA setup, checking posting dates, verifying periods. Meanwhile the culprit is a duration field buried in the scan entry records.

The fix in the open PRs addresses this by handling the 0D edge case before the date calculation runs. If the last scanned duration is zero, the logic either initializes it to a valid default or skips the calculation entirely.

If you're running FA scans on BC 28 and hitting this error, check your FA Scan Entries for records where "Last time scanned" is blank or 0D. Manually setting a valid value on those entries will unblock you until the fix ships.

Have you encountered cryptic date validation errors in Fixed Assets?

> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open Business Central and navigate to FA Scan Entries
> 2. Find a record where "Last time scanned" shows 0D or blank
> 3. Capture the error message "The date is not valid" when running the scan
> 4. Annotate the zero-duration field with a box or arrow

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Fix PR (main): FA Scan entries date not valid — 0D duration](https://github.com/microsoft/BCApps/pull/6964)
- [Fix PR (28.x): FA Scan entries date not valid](https://github.com/microsoft/BCApps/pull/6963)
- [Fix PR (28.0): FA Scan entries date not valid](https://github.com/microsoft/BCApps/pull/6962)
