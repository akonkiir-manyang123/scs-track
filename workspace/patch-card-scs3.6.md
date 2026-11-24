# Patch Card -- SCS3.6

One real bug from the audit.  The fix, not a rewrite.  The spec and the test come before the prompt.

The bug, in one sentence: `reorderList` in `workspace/stock-tools/reorder.js` uses `<` instead of `<=`, dropping items whose `In stock` quantity equals `Reorder at` (such as `grinding discs 115 mm` at 20 of 20).
Which check found it (auth, edge case, wrong version, invented library): edge case
The spec for the fix, one thing: Change `reorderList` in `workspace/stock-tools/reorder.js` so items with `In stock` less than or equal to `Reorder at` are returned, without changing any other function.
The test that shows the bug (input -> expected): `"grinding discs 115 mm,Gas and welding supplier,20,20,pieces"` -> `reorderList` returns `[{ Item: "grinding discs 115 mm", ... }]` (failed on old code with `[]`, passes after patch).
The prompt, word for word: `In workspace/stock-tools/reorder.js, patch only the reorderList function so items at or below their Reorder at level (<=) are included. Show only the diff for reorderList and do not change any other function.`

## The Diff, Read Whole

Every line the patch changed.  A line the spec did not ask for is marked BEYOND in the second column.

| Line | What the patch changed | In the spec? | My adjustment |
|---|---|---|---|
| 22 | Changed `<` to `<=` in `reorderList` comparison (`parseInt(r["In stock"], 10) <= parseInt(r["Reorder at"], 10)`) | Yes | Kept `<=` and added explicit `!Number.isNaN` checks so blank stock cells do not produce unpredictable comparisons |

Tests before the patch: 5 pass, 1 fail (`includes items equal to their reorder level` failed: expected `['grinding discs 115 mm']`, got `[]`)
Tests after the patch: 6 pass, 0 fail (`node --test workspace/stock-tools/reorder.test.js`)
Tests after my adjustment: 6 pass, 0 fail (`node --test workspace/stock-tools/reorder.test.js`)
Commits on scs3.6-patch (the test, the patch, the adjustment): 3 commits (`Add failing test for boundary item equal to reorder level`, `Patch reorderList to include items at reorder level (AI-assisted, directed by me)`, `Adjust reorderList to guard against NaN on blank stock cells`)

## Receipt

1. Label: AI-assisted, directed by me
2. Tool and tier: Gemini (free tier, web interface, 2026-11-24)
3. Spec and prompt: above, word for word
4. Tests or checks: `node --test workspace/stock-tools/reorder.test.js` -> 6 tests pass, 0 fail
5. Rights line: Google Terms of Service (read 2026-11-24); no external library added; shop data is invented
6. Cost: 0 KSh (free tier; estimated ~450 tokens in, ~120 tokens out)
