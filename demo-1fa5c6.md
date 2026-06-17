# Hugo: distinct 'sent' states for SAP write-back (awaiting / ack'd / rejected)

Fix silent SAP write-back failures (DRY-1287). Today 'sent' is set at our IDoc handoff, before SAP acknowledges; rejected POs and connection drops live invisibly in the buyer queue.

Changes:
- Three states: sent (awaiting SAP ack) → sent (SAP ack'd) / sent (SAP rejected).
- Subscribe to outbound IDoc status updates on the existing RFC channel.
- 30-min no-ack soft-alert.
- Buyer queue surfaces ack'd vs awaiting; rejected POs get a red banner with the SAP error.
- Migration sweeps the last 30d of 'sent' POs across all orgs to backfill the new states.

Reported by Brenner and Aldritch within 24h via Fathom calls; both learned of write-back failures from suppliers, not from Hugo.
