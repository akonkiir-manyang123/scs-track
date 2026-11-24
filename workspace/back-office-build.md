# Kiosk Back Office Build Notes

## Overkill test
| Question | Client Answer |
| :--- | :--- |
| 1. How many items or accounts are tracked? | Under 30 kiosk stock items. |
| 2. How many people enter transactions daily? | 1 owner and 1 shop attendant on a single shared sheet. |
| 3. Does the business need automated customer billing or tax APIs? | No, cash and M-Pesa retail kiosk sales only. |
| 4. Can the owner maintain basic spreadsheet rows after setup? | Yes, the owner already records daily sales in a notebook. |
| 5. Would custom software cost more time/money than the problem justifies? | Yes, custom software is unnecessary overhead for a single kiosk. |

Verdict: Sheets.  Pattern: Stock ledger (IN / OUT).  Because: The owner only tracks under 30 items at one kiosk and needs simple daily stock totals with zero software cost.

## Validation and protection
- Rule 1 (ITEM dropdown): Typed `InvalidItem` -> rejected by strict Reject-input rule.
- Rule 2 (DIRECTION dropdown): Typed `MAYBE` -> rejected by strict Reject-input rule.
- Rule 3 (QUANTITY/PRICE numbers): Typed `abc` -> rejected by strict Reject-input rule.
- Protection range 1: `Dashboard!A1:F20` (restricted to owner only).
- Protection range 2: `Lists!A1:C20` (restricted to owner only).
- Protection range 3: `Records!F2:F` calculated AMOUNT column (warn/restrict manual edits).

## AI receipts
| Tool / Prompt | Formula Suggested |
| :--- | :--- |
| Gemini (Chrome side panel) | `=SUMIFS(Records!$D$2:$D, Records!$B$2:$B, A4, Records!$C$2:$C, "IN")` |
| Gemini (Chrome side panel) | `=SUMIFS(Records!$D$2:$D, Records!$B$2:$B, A4, Records!$C$2:$C, "OUT")` |
| Gemini (Chrome side panel) | `=SUMIFS(Records!$F$2:$F, Records!$B$2:$B, A4, Records!$C$2:$C, "OUT")` |
| Gemini (Chrome side panel) | `=IF(D4<10, "REORDER", "")` |

## Break the books
| Attack | What I said would happen | What happened | Held or the fix |
| :--- | :--- | :--- | :--- |
| 1. Type invalid item name on Records | Validation rejects the entry | Blocked with invalid input error | Held |
| 2. Type text into QUANTITY column | Validation rejects non-numeric text | Blocked with invalid input error | Held |
| 3. Type invalid direction (`SOLD`) | Validation rejects anything except IN/OUT | Blocked with invalid input error | Held |
| 4. Overwrite a Dashboard formula cell | Sheet protection blocks non-owner edit | Blocked edit attempt on Dashboard | Held |
| 5. Leave trailing space on item name | SUMIFS misses the row and returns 0 | Returned 0 for Sugar and Pencils | Fixed using Data cleanup > Trim whitespace |
| 6. Enter text date (`1 1/11/2026`) | Treated as text instead of valid date | Failed date check on Row 2 | Fixed locale and retyped as valid date `01/11/2026` |
| 7. Overwrite old row instead of appending | Loses audit trail of original entry | Altered historical figure | Fixed by appending correction row and checking Version History |
