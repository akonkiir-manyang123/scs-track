# Kiosk Back Office Build Notes

## Overkill Verdict
Google Sheets is the right fit here instead of custom software because the kiosk has under 30 SKUs, single-location daily stock entries, and the owner needs zero hosting cost and simple mobile/desktop access.

## Validation and Protection
- Lists tab holds approved ITEM names and DIRECTION values (IN, OUT).
- Records entry columns (DATE, ITEM, DIRECTION, QUANTITY, PRICE, AMOUNT) enforce strict Reject-input data validation rules across all rows.
- Dashboard tab is protected so only the owner/admin can edit formulas while staff only enter rows on Records.

## AI Receipts
Every AI prompt shared only column headers (DATE, ITEM, DIRECTION, QUANTITY, PRICE, AMOUNT) and generic formula structure; no private client transaction figures or exports were pasted into external prompts.

## Break the Books
- Tested typing invalid item names and negative text into Records: rejected by validation.
- Tested typing directly onto Dashboard summary cells as a non-owner editor: blocked by sheet protection.
- Tested appending correction rows instead of overwriting historical rows: totals updated cleanly while preserving Version History.
