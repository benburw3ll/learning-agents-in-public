# Story 13.3: The lifecycle and the one-PR rule

Time: about 45 minutes. Prerequisite: story 13.2.

## Goal

Run a read-only swarm through every step, from clearing the field to the report, and learn why each "once" rule exists.

## Afterward you can explain

- The ten steps, and which two happen at the same time
- Why every member launches in one message
- Why a swarm gathers once, gates once, reviews once and opens one PR
- How a read-only swarm "gathers" when nothing was committed

## Key ideas

| Step | What | Why it exists |
| --- | --- | --- |
| 0 Clear the field | `busy.sh` lists files other worktrees and open PRs already hold | a lane that edits a held file collides with someone else's PR later |
| 1 Pick the preset | say the roster in one line: "QA swarm: 3 scouts (money math, promises, tests)" | names the pieces before anything is spent |
| 2 Branch | the swarm's own worktree and branch off `origin/main` | other sessions may be using the main checkout |
| 3 Lanes | `lanes.sh <name>...`: one worktree per builder | writers need separate folders; readers share the checkout |
| 4 Launch | every member in one message | members launched one message at a time run one after another |
| 5 Lead's share | the lead does the piece that needs the most context while members run | an idle lead wastes the parallel time; polling wastes tokens (you're notified) |
| 6 Gather | `gather.sh` cherry-picks the lanes back; read-only swarms gather by the lead applying recommendations | one place where everything meets |
| 7 Gate and review | the full test suite once, reviewers once | lanes can pass alone and still break together |
| 8 One PR | merge on green in the background | one CI run, one review, one merge |
| 9 Report | a few lines: who did what, the PR, what was left out | the person reads this, not the transcript |

Why "once": picture a UI swarm where every builder opens its own PR and every pass is a new one. Five screen areas over three passes is fifteen PRs. At 5 to 25 minutes of CI each, plus a review and a merge for each one, that's hours of waiting for one ask. Hence: builders never push or open PRs; gather once, gate once, review once; no re-review after the merge; no second PR for the same ask.

## Guide for the agent

1. Give the learner the ten step names shuffled. They put them in order and say why three of them exist.
   Checkpoint: check the order. Which two steps run at the same time? (4 and 5.)
2. Reset the dojo: `node ~/.claude/skills/swarm-school/labs/seed-dojo.mjs ~/swarm-dojo --reset`.
3. Have the learner write the roster line and three angles for a QA swarm on the dojo.
   Checkpoint: run the overlap test on every pair of angles: could both report the same finding? If they overlap, have them sharpen. The reference trio is money math (`src/money.js`, `src/split.js`); promises in README.md and AGENTS.md against the code; tests and failure paths (what `npm run check` can't see).
4. Have the learner write one brief template for all three scouts: goal, piece, "the others cover", "read AGENTS.md and README.md first", up to 6 findings ranked by cost with file:line evidence, a concrete input and output, and the exact change including the test that would catch it, "no style notes", never ask, under 400 words. Launch the three `swarm-scout` members in one message on Sonnet. (The qa preset normally uses Opus scouts; say why Sonnet is fine here.)
5. Lead's share while they run: the learner reads `src/store.js` (about 20 lines) and writes down what looks wrong.
6. When all three report, score them with `dojo-answer-key.md`: distinct bugs found, overlap, ranking, padding. Then show the learner the key and compare their own `store.js` notes with K3 and K4.
   Checkpoint: where did the scouts overlap, and which line in the brief would have prevented it?
7. Gather the QA way: the learner picks the two highest-cost findings and writes the fixes, each with its test, on a branch `fix/qa-lab` in the dojo. Then `npm run check` once.
8. The "PR": `git -C ~/swarm-dojo push -u origin fix/qa-lab`. Say what happens for real: one PR, merge on green in the background, keep working.
   Checkpoint: the PR merged, and a review comment you missed suggests one more change. New PR? (No re-review after the merge and no second PR for the same ask. If it's a real bug, it goes on the board for the next piece of work.)

Point out when it comes up:

- The dojo's 8 tests were green before the swarm found bugs. Tests only check what someone thought to test; a green gate is not a correct program.
- If the learner checks on the scouts mid-run, there's nothing to do: the session is notified when each one finishes.

## Done when

- [ ] Three scouts launched in one message with non-overlapping angles
- [ ] The swarm found at least 6 of the 10 planted bugs (scored with the answer key)
- [ ] Two fixes with tests landed on `fix/qa-lab`, and the suite passed once
- [ ] You can explain why each "once" rule exists

## Log prompt

How many of the ten bugs did the swarm find, how many did you find in `store.js` alone, and where did the scouts overlap?
