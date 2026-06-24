# Multi-currency: per-supplier contract_currency drives every monetary render

Stop assuming USD across the rendering layer (DRY-1254). EU customers run on EUR contracts and EUR books; Hugo was rendering everything in USD, causing at least one near-miss on an approval limit.

Changes:
- Add suppliers.contract_currency (defaults to per-org primary currency if unset).
- Every monetary render reads source-of-truth currency; optional secondary 'operational' currency display in per-user settings.
- Approval limits become currency-scoped — Stefan's €50k limit is no longer compared against $50k POs.
- Backfill contract_currency on existing suppliers using the modal currency of their last 12 months of invoices.

Reported by Voss (Stefan Hartwig) and Hartmann (Daniel Gerlach) within a day of each other on Fathom calls.
