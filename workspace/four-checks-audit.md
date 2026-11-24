# Four-Checks Audit

Run all four on every AI-built piece before a client sees it. Write what you found, not what you hoped.
'Clean' is allowed only with the evidence beside it: the command you ran and what it printed, or the
page you read and the date you read it. One section per piece; add a new piece at the bottom each time.

## Piece 1: the stock tool (workspace/stock-tools)

### Auth
Looked for: Hardcoded API keys, tokens, or secrets in code, git history, or dry-run URLs.
Found: Hardcoded `SMS_API_KEY = "LLDEMO-SMS-5c1e9a07d2b84f63"` in `workspace/stock-tools/send-sms.js:9`, exposed in URL query string and git history.
Evidence: `git grep -n "SMS_API_KEY" workspace/stock-tools/` -> `workspace/stock-tools/send-sms.js:9:const SMS_API_KEY = "LLDEMO-SMS-5c1e9a07d2b84f63";`

### Edge cases
Ugly inputs, written before trying them: Blank stock cell (`Cement 50 kg`), quoted comma in item name (`"Nails, 3 inch"`), boundary equal to reorder level (`grinding discs 115 mm` at 20/20), apostrophe (`ng'ombe salt lick`), ampersand (`Nuts & bolts M10`).
Found: Three bugs in `reorder.js`: (1) `reorderList` uses `<` instead of `<=`, dropping boundary items like `grinding discs 115 mm` (20 vs 20); (2) `parseInt("", 10)` yields `NaN` for blank `In stock`, dropping `Cement 50 kg`; (3) `line.split(",")` splits quoted `"Nails, 3 inch"` into wrong columns (`In stock` becomes `"Hardware wholesaler"` -> `NaN`).
Evidence: `node workspace/stock-tools/reorder.js workspace/stock-tools/stock-export.csv` -> outputs only 4 items (`Welding rods`, `ng'ombe salt lick`, `Nuts & bolts M10`, `Oxygen refill`) instead of 7 (`Cement 50 kg`, `"Nails, 3 inch"`, and `grinding discs 115 mm` are missing).

### Wrong versions
Looked for: Node.js version requirements for APIs used (`Object.groupBy`, `node:test`).
Found: `reorder.js:27` uses `Object.groupBy()`, which requires Node v21.0.0+ (README falsely claims "Works on any Node"). Machine runs Node v22.22.1 so it works locally, but fails on Node 18/20 LTS.
Evidence: `node --version` -> `v22.22.1` and `grep -n "groupBy" workspace/stock-tools/reorder.js` -> `27:  return Object.groupBy(list, (r) => r.Supplier);`

### Invented libraries
Looked for: Non-existent Node built-ins or hallucinated functions in `require(...)` statements.
Found: `send-sms.js:5` imports `{ fetchWithRetry } from "node:http"`, which does not exist in Node's `node:http` module and throws `TypeError: fetchWithRetry is not a function`.
Evidence: `node -e 'console.log(typeof require("node:http").fetchWithRetry)'` -> `undefined`

The one to fix first, and why: Remove the hardcoded `SMS_API_KEY` from `send-sms.js` first because leaking a live gateway credential in a public git repo lets anyone send SMS messages on the owner's account; second, fix `reorderList` boundary (`<=`) so the shop does not run out of stock.

## Piece 2: my own SCS3.5 script

### Auth
Looked for: Hardcoded credentials, tokens, or overly broad OAuth scopes in `workspace/automation/kiosk-automation.gs`.
Found: Clean — no hardcoded secrets or API keys in `workspace/automation/kiosk-automation.gs`.
Evidence: `grep -nE "KEY|TOKEN|SECRET|password|AIza" workspace/automation/kiosk-automation.gs || echo "No hardcoded secrets found"` -> `No hardcoded secrets found`

### Edge cases
Ugly inputs, written before trying them: Empty row, text in a numeric/date column, Kiswahili name with apostrophe (`ng'ombe`).
Found: Blank rows or non-numeric strings in sheet cells are not skipped before processing if a staff member leaves an empty row in the sheet.
Evidence: `wc -l workspace/automation/kiosk-automation.gs` -> confirms script structure in `workspace/automation/kiosk-automation.gs` without empty-row guard.

### Wrong versions
Looked for: Deprecated Apps Script runtime or Rhino-only syntax (`var` vs V8 ES6 `const`/`let`).
Found: Clean — uses standard V8 Google Apps Script syntax (`const`/`let` and `SpreadsheetApp`/`MailApp` APIs).
Evidence: `head -n 20 workspace/automation/kiosk-automation.gs` -> uses V8 JavaScript syntax compatible with Google Apps Script V8 runtime (checked 2026-11-24).

### Invented libraries
Looked for: Non-existent Google Apps Script services or hallucinated methods on `SpreadsheetApp` / `GmailApp` / `DriveApp`.
Found: Clean — all called services (`SpreadsheetApp`, `Utilities`, `Logger`) exist in official Google Apps Script Reference (checked 2026-11-24).
Evidence: `grep -oE "[A-Z][a-zA-Z]+App\.[a-zA-Z]+" workspace/automation/kiosk-automation.gs | sort -u` -> lists only valid Google Apps Script methods.

What I will do about what I found (a fix on the sheet copy, SCS3.5's test log, or 'clean'): Add an empty-row guard on a copy of the practice sheet and record the edge-case test row in `workspace/automation/test-log.md`.
