---
title: "Business Central custom API page: PATCH 404 on singular endpoint with composite ODataKeyFields"
date: 2026-10-29T09:00:00+01:00
draft: false
slug: "business-central-custom-api-page-patch-404-on-singular-endpoint-with-composite-odatakeyfie"
tags: ["business-central", "businesscentralapi", "problem"]
description: "Do you test the keyed record GET before investigating a PATCH payload?"
---

A successful filtered GET does not prove your PATCH addresses the same resource.

A Business Central custom API question reports a working collection GET on warehouseActivityLines, but a PATCH 404 on warehouseActivityLine(...).

The page declares:
EntityName = 'warehouseActivityLine';
EntitySetName = 'warehouseActivityLines';

That singular/plural difference is worth checking before blaming sandbox metadata caching.

Inspect the published $metadata and compare the entity set and key declarations with the request. Test a record GET using the declared entity set and composite key before retrying an update.

This is a proposed diagnostic check, not a reproduced resolution of the question. A filtered collection GET confirms that the filter returns a record; it does not validate the keyed URL used by PATCH.

The question's only answer suggests removing key property names. It is not accepted, so I would not present that suggestion as a confirmed fix either.

Microsoft's custom API guide recommends a single GUID key for integration compatibility, but also documents composite keys. Composite ODataKeyFields alone are not proof of an invalid API.

Do not redesign an existing API's key just to bypass an unexplained 404. First establish which request fails and why.

Do you test the keyed record GET before investigating a PATCH payload?

---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [Original question: collection GET and singular PATCH](https://stackoverflow.com/questions/79858253/business-central-custom-api-page-patch-404-on-singular-endpoint-with-composite)
- [Unaccepted answer: key syntax suggestion](https://stackoverflow.com/a/79878698)
- [Microsoft Learn: Developing a custom API](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-develop-custom-api)
