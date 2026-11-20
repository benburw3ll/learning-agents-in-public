# Dojo answer key (for the tutor, and for after a lab)

Never paste this into a member's brief and never copy it into the dojo: scouts would read it and the lab would prove nothing. Show it to the learner after a lab, to score the swarm.

The dojo's gate (`npm run check`, 8 tests) is green at seed while every bug below is live. That is story 13.3's point: a green gate is not a correct program.

| # | Where | What is wrong | Kind | Cost (rank) | Board issue |
| --- | --- | --- | --- | --- | --- |
| K1 | `src/split.js` splitEvenly | `Math.floor` drops the remainder: 1000 / 3 → 333 × 3, payer short a cent; README promises exact shares | correctness, docs | high | #1 |
| K2 | `src/money.js` parseAmount | `parseFloat("1,200.00")` → 1 → 100 cents; `"12abc"` → 1200; README promises "1,200.00" | correctness, docs | high | #2 |
| K3 | `src/store.js` load | no file yet → ENOENT crash on first `add`; README: "created on first use" | correctness, docs | high | #3 |
| K4 | `src/store.js` fileFor | group name joined unchecked: `../../x` writes outside `$POTLUCK_HOME`; AGENTS.md forbids it | security, rules | high | #5 |
| K5 | `src/dates.js` isOverdue | `>= 0` marks the due day itself overdue; README: "the day after" | docs vs code | medium | #4 |
| K6 | `src/cli.js` default | unknown command returns code 0; README: code 1 | docs vs code | medium | #6 |
| K7 | README / `src/cli.js` | `--currency` documented, never parsed | docs drift | medium | #7 |
| K8 | `test/*` | tests cover only even splits, plain amounts, existing files, days after the due date: the gate cannot see K1–K6 | tests | medium | (none) |
| K9 | `src/money.js` formatCents | negative → `$-5.00` instead of `-$5.00`; nothing passes a negative today | correctness | low | (none) |
| K10 | `src/cli.js` | missing arguments (`potluck add trip`) throw a raw stack trace; no try/catch in the entry point | UX | low | (none) |

Not bugs, and a scout that reports them as findings is padding: parseAmount called twice in `add` (harmless), no dependency injection, "should use TypeScript", style.

## Scoring a QA lab

- **Found:** count distinct K-numbers across all reports. A good 3–4 scout swarm on sonnet finds 6–8 of the 10; K1, K2, K3 nearly always.
- **Overlap:** a K found by 2+ scouts is overlap. Some is fine (it confirms); 3+ scouts on the same K means the angles overlapped and the brief should have split them better.
- **Rank quality:** K9 ranked above K1–K4 is a ranking miss (a cosmetic bug over a money bug).
- **Fix quality:** a finding is only "applicable" if it names the file, the exact change and a test. "Consider improving error handling" is not applicable.
- **Padding:** count the not-bugs. More than one per report means the brief needed a "no style, no maybes" line.

## Reference fixes (for the build lab review)

- K1: `const base = Math.floor(total / people), extra = total % people; return Array.from({ length: people }, (_, i) => base + (i < extra ? 1 : 0));`
- K2: `if (!/^(\d{1,3}(,\d{3})+|\d+)(\.\d{1,2})?$/.test(String(text ?? '').trim())) throw …; const value = Number(text.replace(/,/g, ''));`
- K3: catch `err.code === 'ENOENT'` in `load` → `{ payments: [] }`; rethrow anything else.
- K4: `if (!/^[A-Za-z0-9-]+$/.test(group ?? '')) throw new Error('group names use letters, digits and dashes');` before `join`.
- K5: `> 0`.
- K6: `return { code: 1, out };` in `default`.
- K7: a product call. Implementing it touches `cli.js` (parse the flag) and passes the code to `formatCents`; dropping it touches README only. Either is fine if the report says which and why.

## The build lab's file split (the one that works)

| Lane | Owns | Board issues |
| --- | --- | --- |
| `money` | `src/money.js`, `src/split.js`, `test/money.test.js`, `test/split.test.js` | #1, #2 |
| `cli` | `src/store.js`, `src/dates.js`, `src/cli.js`, `test/dates.test.js`, `test/cli.test.js`, new `test/store.test.js` | #3, #4, #5, #6 |
| lead | `README.md`, `CHANGELOG.md`, `BOARD.md` | #7 (the product call), the changelog lines |

The tempting wrong split is "builder A takes #1–#3, builder B takes #4–#7" (by issue count): #3 (lane A) and #5 (lane B) both edit `store.js`, so the two lanes touch the same lines and gather conflicts. Split by files, then see which issues land where.
