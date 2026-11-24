# GEMINI.md

## Stack
Node.js v22 CommonJS CLI scripts (`workspace/stock-tools/`) and Markdown operational docs/logs for the reference hardware and welding shop.
No external npm packages; uses built-in `node:fs`, `node:test`, and `node:assert`.

## Tests
`node --test workspace/stock-tools/reorder.test.js`

## Never
- Never hardcode API keys, tokens, or credentials in code or commit `.env` files; always read secrets from `process.env`.
- Never import unverified or invented Node built-ins (such as `fetchWithRetry` from `node:http`) without checking official Node docs first.
- Never paste real client names, phone numbers, or customer records into prompts or public repo files; use invented rows only.
- Never rewrite an entire file when asked to patch a single function.

## Skills
- `skills/weekly-stock-audit/SKILL.md` — Weekly stock reorder check and dry-run verification.
