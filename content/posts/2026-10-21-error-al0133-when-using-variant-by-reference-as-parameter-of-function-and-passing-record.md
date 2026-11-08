---
title: "Error AL0133 when using Variant by reference as parameter of function and passing record"
date: 2026-10-21T09:00:00+01:00
draft: false
slug: "error-al0133-when-using-variant-by-reference-as-parameter-of-function-and-passing-record"
tags: ["aldevelopment", "business-central", "problem"]
description: "Have you used this Variant round trip, and did your caller need fields, filters, or both?"
---

You can waste hours on AL0133 when the workaround is one Variant variable.
But getting it to compile is not the same as getting full by-reference behaviour.

GitHub issue #5030 documents the problem in AL Language 3.0.124247.
A function accepts a `var Variant`, but passing a record directly produces AL0133:

`Argument 2: cannot convert from 'Record "tablename"' to 'var Variant'`

The intention is straightforward.
Accept any record, modify it, and return the changes through the parameter.

But the direct record argument is rejected.

To confirm the reported problem, define a function with a `var Variant` parameter and call it with a record.
Check the Problems panel in VS Code for AL0133 at that argument.

The issue describes this workaround:
Assign the record to a Variant variable.
Pass that variable to the function.
Assign the Variant back to the record after the call.

However, a follow-up test in the same thread exposes the limit.
Field changes survive the round trip.
Filter changes do not propagate back.

So this is a workaround for returning changed field values, not a substitute for every behaviour of a typed `var Record` parameter.

Before accepting the fix, check what the caller actually needs back.
If it needs changed filters too, compiling successfully is not enough.

This is a historical report, not proof that every current compiler behaves identically.

Have you used this Variant round trip, and did your caller need fields, filters, or both?

## The exact code

```al
local procedure TestVariantCall()
var
    Customer: Record Customer;
    RecordVariant: Variant;
begin
    ProcessRecords(Customer, Customer);
    RecordVariant := Customer;
    ProcessRecords(Customer, RecordVariant);
    Customer := RecordVariant;
end;

local procedure ProcessRecords(InputRecord: Variant; var OutputRecord: Variant)
begin
end;
```


---

Originally published as a shorter post on [LinkedIn](https://www.linkedin.com/in/ricardo-carvalho-bc/). Sources backing every claim above:

- [Microsoft AL issue #5030: var Variant record argument error and workaround limitations](https://github.com/microsoft/AL/issues/5030)
