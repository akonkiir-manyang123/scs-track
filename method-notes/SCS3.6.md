1. Reading the stock tool line by line revealed three silent bugs that passed all five original unit tests.
2. Writing ugly inputs first (blank cells, quoted commas, boundary equalities, and Kiswahili apostrophes) exposed where CSV parsing and threshold logic failed.
3. Removing the hardcoded `SMS_API_KEY` by hand kept the credential out of AI prompts while teaching why leaked git history still requires key rotation.
4. Scoping the patch to one function with three separate commits made the diff easy to verify and defend line by line.
5. Pairing a repository rules file (`GEMINI.md`) with a scoped agent branch kept AI edits bounded and auditable.
6. The check I ran least carefully on my own patch was edge cases for quoted commas in CSV cells (`"Nails, 3 inch"`), and a unit test passing `"Nails, 3 inch,Hardware wholesaler,4,10,kg"` into `parseCsv` would tell me immediately whether `row["In stock"]` parses as `"4"` instead of `"Hardware wholesaler"`.
