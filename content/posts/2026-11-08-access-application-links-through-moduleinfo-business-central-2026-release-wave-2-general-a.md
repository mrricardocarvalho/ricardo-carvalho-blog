---
title: "Access application links through ModuleInfo (Business Central 2026 release wave 2, General availability)"
date: 2026-11-08T09:00:00+01:00
draft: false
slug: "access-application-links-through-moduleinfo-business-central-2026-release-wave-2-general-a"
tags: ["aldevelopment", "business-central", "what-s-coming"]
description: "Do your extensions read these links from the app, or maintain another copy?"
---

ModuleInfo can now tell you where an app's help and legal information live.

Business Central Update 29.0 lists "Access application links through ModuleInfo" as generally available, under Roadmap ID 573354.

The method documentation gives that headline a precise scope:

Help() returns the application's help link.
EULA() returns its End User License Agreement link.
PrivacyStatement() returns its privacy statement link.
ContextSensitiveHelpUrl() returns its context-sensitive help URL.

The last one has an important detail: it resolves the user's locale from the application's supported locales.

For a multilingual extension, checking the help destination therefore means checking the locale as well as the base URL.

These four methods require runtime 18.0. ModuleInfo itself is older, so the data type's original runtime is not the compatibility check to use.

My practical review would start with code that duplicates these help or legal URLs. Compare it with the application's metadata, then assess whether the new methods can replace that duplication.

Check your app’s target runtime before introducing the calls. Then test the returned links and relevant user locales in your target environments.

Do your extensions read these links from the app, or maintain another copy?

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [Update 29.0: release announcement](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/whatsnew/whatsnew-update-29-0)
- [ModuleInfo data type: method overview](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/moduleinfo/moduleinfo-data-type)
- [ModuleInfo.Help(): help link and runtime](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/moduleinfo/moduleinfo-help-method)
- [ModuleInfo.EULA(): EULA link and runtime](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/moduleinfo/moduleinfo-eula-method)
- [ModuleInfo.PrivacyStatement(): privacy link and runtime](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/moduleinfo/moduleinfo-privacystatement-method)
- [ModuleInfo.ContextSensitiveHelpUrl(): locale resolution and runtime](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/moduleinfo/moduleinfo-contextsensitivehelpurl-method)
