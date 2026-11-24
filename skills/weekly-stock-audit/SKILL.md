# Skill: Weekly Stock Reorder Check

**Name:** weekly-stock-audit
**When to use:** Every Monday morning before placing supplier orders from `workspace/stock-tools/stock-export.csv`.

## Steps
1. Export the latest stock sheet as CSV into `workspace/stock-tools/stock-export.csv`.
2. Run the automated unit tests: `node --test workspace/stock-tools/reorder.test.js`.
3. Run the reorder script: `node workspace/stock-tools/reorder.js workspace/stock-tools/stock-export.csv`.
4. Verify no secrets are exposed in dry-run mode: `SMS_API_KEY=test-key node workspace/stock-tools/send-sms.js workspace/stock-tools/stock-export.csv --dry-run`.
5. Send the grouped reorder list to each supplier via WhatsApp.

## How you know it worked
All 6 unit tests pass with exit code 0, and every item at or below its `Reorder at` threshold appears grouped under its supplier.

Ran: 2026-11-24 — `node --test workspace/stock-tools/reorder.test.js` printed `pass 6, fail 0` and dry-run verified environment variable lookup.
