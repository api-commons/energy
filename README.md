# Energy and Utilities

The common utility-data vocabulary -- the meters on a premises, the readings and interval usage they record, the utility accounts and bills they roll up into and the tariffs that price them -- distilled from the APIs that already exist, energy-sector open-data standards included. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Utilities, Electricity, Smart Metering, Utility Data, Energy Data, Energy Management, Green Button, Electric Utilities in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| meter | 15 | 11 | id 55% | meters 12, meter 2, servicepoints 1 |
| meter_reading | 8 | 6 | end_at 50%, start_at 50%, unit 50% | intervals 4, readings 2, usage 1, consumption 1 |
| utility_account | 5 | 4 | id 100%, created_at 75% | accounts 5, account 1 |

Cohort: 95 providers with harvested OpenAPI, 25 crosswalks. Of the providers exposing a meter: 40% create, 93% list, 67% fetch, 40% update, 20% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Eleven Australian retailers and regulators publish the same Consumer Data Right energy standard; counted once, the open market is thin. Meters agree only on id -- status, meter_type and number each reach a third of providers.
- Meter readings agree on start and end and unit: an interval with a unit is the shared shape, the value field is spelled differently by every provider.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The CDR energy standard counts as one voice (au-cdr-energy), as the banking standard did; without that, its servicepoint vocabulary would be the core of the context.
- Bills were dropped: two readable schemas share nothing. Utility accounts stay at extended, with the meter they belong to as the required parent.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
