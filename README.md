# cloud-itonami-lei-5299008fntq0ldq3uz44

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by G8 Education Limited.**

This repository archives publicly published legal/policy documents of
**G8 Education Limited**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.edn)
and [ADR-2607199960](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607199960-cloud-itonami-lei-top10-universe-expansion.edn)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: G8 Education Limited
- **LEI (ISO 17442)**: [5299008FNTQ0LDQ3UZ44](https://search.gleif.org/#/record/5299008FNTQ0LDQ3UZ44) (GLEIF-verified)
- **Jurisdiction**: AU
- **Website**: https://www.g8education.edu.au

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived documents, each entry
  carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`, `:tos/sha256`,
  `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage. See ADR-2607110300's sibling isco-progress file (`2607110300-cloud-itonami-lei-corporate-tos-catalog.isco-progress.edn`) for why this company was added under isco-1341 (Independent Child Care Services Management Practice) top-up depth expansion (2026-07-19, iteration 3). No general consumer Website Terms of Use was discoverable on this ASX-listed operator's corporate site (checked multiple guessed paths and the site's XML sitemap); the Privacy Policy was used as the closest real, substantive published legal document, honestly recorded as :privacy-policy not :terms-of-service.
