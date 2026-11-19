# Test log -- SCS3.5

The expected answers below are worked out by hand before running the script. All test information is made up.

| Case | Input rows (made up) | Expected (by hand, before the run) | Actual (after the run) | Pass or fail | Patch (line, commit) |
|---|---|---|---|---|---|
| Test 1 | DASHBOARD: Milk, stock 2, status REORDER; Sugar, stock 20, status OK. | REMINDERS should contain the headings ITEM, CURRENT STOCK, STATUS, followed by Milk, 2, REORDER only. | REMINDERS showed Milk, 2, REORDER under the three headings. | PASS | No patch needed. |
| Test 2 | RECORD: 05/11/2026, Milk, OUT, sales 500, units 5. | MONTHLY REPORT should show November 2026, total sales 500, and units sold 5. | Report showed November 2026, 500, and 5. | PASS | No patch needed. |
| Edge case | DASHBOARD: all four items have status OK. | REMINDERS should contain the three headings and no item rows. | Only the three headings appeared; no item rows. | PASS | No patch needed. |
| Second edge case (optional, SGL menu) | Not tested yet. | Not decided yet. | Not tested yet. | Not tested yet. | None yet. |
| Partner as a careless owner | Not tested yet. | To be completed with a partner. | Not tested yet. | Not tested yet. | None yet. |
| Re-run in front of the trainer | Not tested yet. | To be completed in front of the trainer. | Not tested yet. | Not tested yet. | None yet. |
