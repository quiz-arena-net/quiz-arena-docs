# UsageTerms

Value object. The terms under which a quiz may be used outside this service. Shown to users so they
know what they may do with it. Use within the service is covered by the terms of service.

- `AllRightsReserved`: no reuse. The default under copyright law, and the right value when no terms
  were found.
- `CreativeCommons(..)`: a [`CreativeCommons`](creative-commons.md) license or dedication.
- `PublicDomain`: the work is in the public domain by law.
- `Custom(..)`: terms the rights holder wrote out, see [`CustomTerms`](custom-terms.md).

`requires_attribution` is derived: true for every Creative Commons license, false for CC0, public
domain and all rights reserved, as stated for custom terms. It concerns reuse by users, not the
credit of an external source, which is always shown.
