# cloud-itonami-lei-529900gql5x8h7ao3t64

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Simon Property Group, Inc..**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Simon Property Group, Inc.**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Simon Property Group, Inc.
- **LEI (ISO 17442)**: [529900GQL5X8H7AO3T64](https://search.gleif.org/#/record/529900GQL5X8H7AO3T64) (GLEIF-verified)
- **Jurisdiction**: US-IN — the live GLEIF record (last updated 2026-07-22) places the
  entity in Indiana, registered with the Business Services Division of the Indiana
  Secretary of State (`RA000609`, registration `202505151891212`, a 2025 filing).
  This README previously said US-DE; `facts.edn` below carries the registry's answer
  with provenance, and the checker flags US-DE as drift today.
- **Website**: https://www.simon.com
- **Ticker**: SPG (NYSE)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 21 verified registry facts with per-fact provenance (9 about the
  entity, its registration, issuer, legal form, securities count, children count and
  both parent-reporting exceptions; 12 one-per-ISIN). **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind
them. `facts.edn` now carries them as data, and every value in it was read out of
a public registry response whose URL and retrieval time sit next to the value:

```
nbb scripts/verify-facts.cljk           # check the recorded facts against the live sources
nbb scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T06:09Z, golden copy 2026-08-22T16:00Z) — the LEI record (legal name
`SIMON PROPERTY GROUP, INC.`, jurisdiction `US-IN`, entity **ACTIVE**,
registration **ISSUED** with the next renewal due 2027-07-25, last updated
2026-07-22, `FULLY_CORROBORATED`, conformity flag `CONFORMING`; entity status
and registration status are different fields and are recorded separately), its
**12 ISINs**, read from `meta.pagination.total` of a 15-per-page request — the
whole list fits in that single page, so each identifier is also mirrored as its
own `:security` entity (the `:source/note` on the count says whether the list
under a count is mirrored or only counted, so a bare count is never ambiguous)
— its managing LOU and LEI-issuer accreditation (Bloomberg Finance L.P., LEI
`5493001KJTIIGC8Y1R12`, marketing name Bloomberg, accredited 2017-04-13),
registration authority `RA000609` (Business Services Division (Secretary of
State), Indiana, registration number `202505151891212`), ISO 20275 legal form
`R0BI` (`For-Profit Corporation`, US-IN), reporting exceptions at both
consolidation levels (`NON_CONSOLIDATING` — the entity does not prepare
consolidating financial statements above itself in GLEIF's relationship data),
and **0 direct children**, read from `meta.pagination.total` of the cited page —
a measured zero, not an unasked question. The `direct-parent` and
`ultimate-parent` endpoints answered `404` because GLEIF publishes the exception
side of that pair for this entity, which the checker treats as a fact rather
than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the
live sources, `1` a citation broke or a fact drifted, `3` the check could not be
performed at all — an absent `facts.edn`, or every request failing at the
transport level. A check that could not run must not be indistinguishable from a
check that ran and found nothing, so it refuses to report a pass rather than
exiting 0. All outcomes were exercised before this landed: unmodified `0`;
`:securities/isin-count` edited `12` → `13` → `1` naming
`DRIFT gleif-isins :securities/isin-count`; the `gleif-isin-us8288068856`
entity deleted → `1` naming `ADDED gleif-isin-us8288068856`; that same entity's
`:securities/isin` value rewritten to a non-existent identifier → `1` naming
`DRIFT gleif-isin-us8288068856 :securities/isin`; the measured zero
`:relationship/direct-child-count` rewritten `0` → `1` → `1` naming
`DRIFT gleif-direct-children-count`; `:company/jurisdiction` rewritten back to
the stale `US-DE` this README used to claim → `1` naming
`DRIFT gleif-lei-record :company/jurisdiction`; the GLEIF host in the checker
rewritten to an unresolvable name → `3` (`INCONCLUSIVE … refusing to report a
pass`).

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
