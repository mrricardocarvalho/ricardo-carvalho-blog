---
title: "Publish Error Cancel Clears Debug Console"
date: 2026-03-02T09:00:00+01:00
draft: false
slug: "publish-error-cancel-clears-debug-console"
tags: ["al", "business-central", "debugging", "quick-tip", "vscode"]
description: "Publishing your AL app failed? Don't click Cancel on the error dialog. It also wipes your Debug Console output."
---

Publishing your AL app failed? Don't click Cancel on the error dialog. It also wipes your Debug Console output.

When a publish error occurs in VS Code, the AL extension shows a dialog. If you dismiss it by clicking Cancel, the Debug Console gets cleared. Any diagnostic output, error details, or trace logs you needed to investigate the failure are gone.

Click the other button or close the dialog differently to preserve your debug output. Or copy the Debug Console content before dismissing.

This is tracked as an open issue on the AL repo.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Cancelling publish error dialog clears the Debug Console](https://github.com/microsoft/AL/issues/8133)
