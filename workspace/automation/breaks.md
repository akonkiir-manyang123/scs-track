# The nine breaks -- SCS3.5

Checked against the current script. Items marked "not prevented" still need checking or improvement.

| # | Break | Cannot happen because ... (line) | Found -- patched at (line, commit) |
|---|---|---|---|
| 1 | The header row counted | Not confirmed: line 6 reads A12:C15. Check whether row 12 is a heading or the first data row. | Not patched. |
| 2 | The wrong tab | Lines 5 and 34 look for the DASHBOARD and RECORD tabs. Line 36 stops if RECORD is missing. Line 5 has no missing-tab check. | Not patched. |
| 3 | The number read as text | Line 86 accepts only a number greater than zero. A number stored as text is treated as invalid. | Not patched. |
| 4 | The boundary | Line 6 reads only rows 12 to 15. Line 39 reads only rows 2 to 1000. More rows are not included. | Not patched. |
| 5 | The overwrite | Lines 13 and 58 clear old contents before writing new results. Existing contents on those report sheets can be erased. | Not patched. |
| 6 | The invented piece | Lines 41 and 42 use a fixed month and year: November 2026. The report does not automatically choose the current month. | Not patched. |
| 7 | The silent assumption | Lines 5, 6, 39, 47 and 52 assume the expected sheet names, column positions, date values and OUT status. These must match the spreadsheet. | Not patched. |
| 8 | The trigger that runs too often | Lines 70 and 74 show onEdit runs after edits and continues only on INTAKE. Lines 79 and 84 add more checks. It can still run on qualifying edits to INTAKE. | Not patched. |
| 9 | The confident wrong answer | Not tested yet. Lines 47 to 56 select records and calculate totals. Test 2 must check the expected report against the actual result. | Not patched. |

