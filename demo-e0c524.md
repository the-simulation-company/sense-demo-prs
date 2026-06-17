# Hugo over-orders past supplier max-per-PO ceilings

The optimizer reads SKU-level reorder points but doesn't join against the SAP vendor master's `max_order_qty` column when the recommendation lands on a Tier-1 with that constraint set, so Hugo can propose POs above contractual ceilings. Fix extends the constraint set in the MILP build to include vendor max-order-qty and adds a regression check against the SAP fixtures so a future Hugo refactor can't re-introduce the gap.
