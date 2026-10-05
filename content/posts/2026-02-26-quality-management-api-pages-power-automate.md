---
title: "Quality Management Api Pages Power Automate"
date: 2026-02-26T09:00:00+01:00
draft: false
slug: "quality-management-api-pages-power-automate"
tags: ["api", "business-central", "powerautomate", "qualitymanagement", "what-s-coming"]
description: "What's your current approach to automating quality inspections in BC?"
---

Quality Management in Business Central is finally getting API pages and external business events for Power Automate.

This has been a gap for a long time.

If you've ever tried to automate quality inspection workflows — triggering notifications when an inspection fails, pushing results to external systems, or syncing QM data with a data lake — you know the pain. There was no clean API surface. You were stuck with custom pages or direct table access.

Now, with dedicated API pages and external business events landing in BC 28, Power Automate flows can react to quality inspection events natively. No more polling. No more custom webhooks duct-taped to event subscribers.

Why this matters for your architecture:

External business events mean your Power Automate flows get triggered the moment a quality inspection is completed or rejected. That's real-time automation without writing a single line of integration code.

The API pages give external systems — whether it's a QMS, a supplier portal, or a reporting dashboard — a first-class contract to read and write quality data.

If you're running quality processes in BC today, start mapping your current custom integrations against the new API surface. You might be able to retire a lot of glue code.

What's your current approach to automating quality inspections in BC?
> Repro steps for your own environment:
>
> Visual Note (manual action — take this screenshot yourself):
> 1. Open Business Central 28 preview or the release notes documentation
> 2. Navigate to the Quality Management module or API pages list
> 3. Capture the new API pages or the external business events configuration
> 4. Annotate the key endpoints or event names

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above: see the original post.
