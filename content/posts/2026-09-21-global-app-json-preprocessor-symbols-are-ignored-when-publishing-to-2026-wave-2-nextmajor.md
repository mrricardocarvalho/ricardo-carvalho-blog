---
title: "Global app.json preprocessor symbols are ignored when publishing to 2026 Wave 2 (NextMajor)"
date: 2026-09-21T09:00:00+01:00
draft: false
slug: "global-app-json-preprocessor-symbols-are-ignored-when-publishing-to-2026-wave-2-nextmajor"
tags: ["business-central", "nextmajor", "what-s-coming"]
description: "Are you already validating your apps against NextMajor? Did your conditional compilation survive the publish, or did you find this one the hard way?"
---

Everyone assumes the global preprocessor symbols in app.json just travel with the app. Publishing to 2026 Wave 2 (NextMajor) says otherwise.

This one is tracked as issue 8300 on the microsoft/AL repo. When you publish to a NextMajor environment, the global symbols declared in your app.json are ignored.

The compiler evaluates your #if directives as if those symbols were never declared. The branch you expected to be active gets skipped. The branch you meant to exclude gets compiled.

So an app that builds clean on your current version can break, or quietly behave differently, the moment it lands on a 2026 Wave 2 sandbox.

Here is the part that stings. Most of us use conditional compilation exactly to handle version differences. NextMajor is where those differences are the largest. This bug hits precisely where you lean on the mechanism hardest.

What I would do before wave 2 lands:

Stand up a NextMajor sandbox and publish an app that depends on global app.json symbols. Then check which #if branches actually made it into the package. A green publish does not prove the right code ran.

And keep an eye on issue 8300. If it is not fixed before general availability, this stops being a preview curiosity and becomes a wave-day incident.

Are you already validating your apps against NextMajor? Did your conditional compilation survive the publish, or did you find this one the hard way?
---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: - [Global app.json preprocessor symbols are ignored when publishing to 2026 Wave 2 (NextMajor), microsoft/AL issue #8300](https://github.com/microsoft/AL/issues/8300)
