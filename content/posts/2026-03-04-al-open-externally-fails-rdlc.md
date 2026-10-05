---
title: "Al Open Externally Fails Rdlc"
date: 2026-03-04T09:00:00+01:00
draft: false
slug: "al-open-externally-fails-rdlc"
tags: ["al", "business-central", "problem", "rdlc", "reports", "vscode"]
description: "Using the 'AL: Open Externally' keybinding on an RDLC file? It crashes with 'Cannot read properties of undefined (reading 'fsPath').'"
---

Using the "AL: Open Externally" keybinding on an RDLC file? It crashes with "Cannot read properties of undefined (reading 'fsPath')."

The shortcut works fine on AL files but breaks on RDLC report layouts. The AL extension doesn't handle non-AL file types in the Open Externally command, so it tries to read a property that doesn't exist on the file context.

Workaround: right-click the RDLC file in the Explorer panel and use "Reveal in File Explorer" instead. Or open it with the system default from the context menu.

This is tracked as an open issue on the AL repo.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Keybinding for AL: Open Externally fails on RDLC files](https://github.com/microsoft/AL/issues/8174)
