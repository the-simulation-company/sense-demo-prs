# SAP IDoc push drops trailing line items on long POs

The leaner ORDERS05 IDoc segment we adopted three weeks ago caps E1EDP01 (line item) repetition at 12 to match the median PO size on the historical sample. The cap isn't a SAP limit — it's a build-side mistake that quietly truncates orders above ~12 lines. Fix removes the cap and adds a 50-line PO fixture so the regression can't recur.
