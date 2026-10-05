---
title: "Al Debugger Callstack Empty Linux"
date: 2026-03-03T09:00:00+01:00
draft: false
slug: "al-debugger-callstack-empty-linux"
tags: ["al", "business-central", "debugging", "linux", "problem"]
description: "Debugging AL on Linux and your Call Stack and Variables panels are empty when paused on an exception? You're not doing anything wrong. It's a known bu"
---

Debugging AL on Linux and your Call Stack and Variables panels are empty when paused on an exception? You're not doing anything wrong. It's a known bug.

The AL debugger on Linux fails to populate the Call Stack and Variables windows when it breaks on an exception. The debugger pauses correctly, but gives you zero context to work with.

This is tracked as an open issue on the AL GitHub repo. Until it's fixed, use the Debug Console to inspect variables manually with evaluate expressions while paused.

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [AL Debugger: Call Stack and Variables Empty When Paused on Exception (Linux)](https://github.com/microsoft/AL/issues/8150)
