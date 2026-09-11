# ADR-0001: ToSMonitor-LLM ⊣ ToSArchiveGovernor -- a governed actor layered on this archive

- Status: Accepted (2026-07-24)
- Related: [`com-junkawasaki/root` ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.edn)
  (the archive-only design this repo was created under -- unchanged by this
  ADR); [`com-junkawasaki/root` ADR-2607241900](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607241900-cloud-itonami-lei-tos-monitor-actor-pilot.edn)
  (the original 1-repo pilot, on `cloud-itonami-lei-2572ibtt8cczw6au4141`,
  P&G); [`com-junkawasaki/root` ADR-2607242500](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607242500-cloud-itonami-lei-tos-monitor-actor-batch10-round4.edn)
  (the fourth 10-repo validation batch this repo is part of).

## Context

This repository archives the publicly published Privacy Policy of G8
Education Limited, per ADR-2607110300 -- a read-only reference archive. As
part of a fourth 10-repo validation batch extending the
`cloud-itonami-lei-2572ibtt8cczw6au4141` pilot (see ADR-2607241900/
ADR-2607242500 for the full fleet-level design rationale), this repo gains
a governed actor layer on top of the unchanged archive. G8 Education
Limited is the first Australia-jurisdiction company in this actor family.

## Decision

Identical design and code to the pilot and every other repo in this batch
(`src/tosmonitor/{governor,phase,operation,registry,advisor}.cljc` are
byte-for-byte identical across all of them) -- see ADR-2607241900 for the
full rationale of each of the six HARD governor checks, the single
always-escalate `:tos/change-proposal` actuation, and the mock-advisor-only
scope. Only `tosmonitor.store`'s company/baseline demo data is specific to
this repo:

- **Company**: G8 Education Limited, LEI 5299008FNTQ0LDQ3UZ44, website
  `https://www.g8education.edu.au`.
- **Baseline provenance** (real, from this repo's own `80-data/public/
  tos.journal.edn`): source-url `https://g8education.edu.au/privacy-policy/`
  (note: no `www.` prefix, unlike the company's `website` field -- this is
  the real archived value, not "corrected"), retrieved-at `2026-07-19`,
  doc-type `:privacy-policy` (this archive is a Privacy Policy, not a Terms
  of Service).
- **Baseline full text**: a short, hand-written representative excerpt (not
  the real, page-length archived text), with a self-consistent SHA-256
  computed from that excerpt itself -- matching the pilot's own convention
  (ADR-2607241900), not a claim that this is the verbatim archived text.

The archive-of-record (`80-data/public/tos.journal.edn`) is never touched;
`commit-record!` only writes to this actor's own Store.

### First AU-jurisdiction company: `.edu.au` two-part-TLD domain-matching note

`source-domain-mismatch-violations` compares the candidate's `source-url`
domain against the company's own `website` domain using
`tosmonitor.registry`'s naive last-two-dot-label `base-domain` heuristic.
For G8 Education, `website` is `https://www.g8education.edu.au` and the
real archived `source-url` is `https://g8education.edu.au/privacy-policy/`
(no `www.` prefix). Both reduce to the same naive base-domain `edu.au` --
a two-part `.edu.au` TLD, the same class of limitation already documented
in `tosmonitor.registry`'s own docstring for `.co.jp`/`.co.uk` (the TEPCO
company in round 1 exercised the `.co.jp` case). This is not a new bug: the
check still matches correctly here regardless of the `www.` prefix
difference, because both hosts share the `edu.au` suffix under the
existing heuristic. A true two-part-TLD false-negative (e.g. a
`g8education.edu.au` vs. an unrelated `otherschool.edu.au`) remains out of
scope for V1, same as the `.co.jp`/`.co.uk` case.

## Consequences

Same as the pilot (ADR-2607241900) and this round's batch (ADR-2607242500)
-- proves the actor pattern holds for a company in a new jurisdiction (AU)
and a new archived doc-type (`:privacy-policy` rather than
`:terms-of-service`).

## Run

```bash
kbb -M:dev:run     # walk a clean lifecycle + all six HARD-hold checks + a phase-0 hold + a backend swap
kbb -M:dev:test    # governor contract · phase invariants · store parity · advisor smoke
kbb -M:lint        # clj-kondo (errors fail; CI mirrors this)
```
