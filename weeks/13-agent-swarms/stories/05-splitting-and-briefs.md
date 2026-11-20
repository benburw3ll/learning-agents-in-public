# Story 13.5: Splitting the work and writing briefs

Time: about 45 minutes. Prerequisite: story 13.4. No agents: you plan, the tutor grades, story 13.6 runs it.

## Goal

Split a job into pieces that can't collide, and write briefs a cold agent can finish without asking anything.

## Afterward you can explain

- Why readers split by angle and writers split by files
- What a hot file is and who owns it
- What "seam first" means and when you need it
- What every line of the brief template prevents

## Key ideas

**Angles (readers) must be orthogonal.** Cut by concern (correctness / security / tests / UX), by source (code / logs / GitHub / docs) or by question ("is money ever lost?" / "do the docs match the code?"). The overlap test: for each pair, could both report the same finding? If yes, sharpen or merge. Then put "The others cover: …" in every brief. That line does most of the work of preventing duplicates.

**Files (writers) must be disjoint.**

1. List what each issue touches, then group so no file is in two groups. Split by files first and see which issues land where, never the reverse.
2. **Hot files** are the ones every piece wants: `package.json`, lockfiles, a shared index or registry, the changelog, shared styles. Each gets exactly one owner, usually the lead.
3. **Seams:** when two pieces need a shared interface (a type, a function signature, a route name), the lead commits it on the swarm's branch before cutting lanes. Lanes are cut from HEAD, so every builder starts with it.
4. Clear the field first: a file another worktree or open PR holds can't be owned by any lane.

**The brief template:**

```
You are <role> <i> of <n> in a <preset> swarm on <repo> (<checkout path>). Goal: <the goal in one line>.
Your piece: <angle / issues / screen area>. The others cover: <one line>.
Builders: Your lane: <path> on branch <lane branch>. You own these files: <globs>. Done when: <checks>.
The owner is away: never ask, never wait; skip what is blocked and say why. Report in under <N> words.
```

| Line | Prevents |
| --- | --- |
| role, i of n, preset, repo path | working in the wrong place, or thinking it's alone |
| Goal | locally sensible work that misses the point |
| Your piece + the others cover | overlap and gaps |
| Lane and files owned | collisions and edits in the main checkout |
| Done when | stopping early or gold-plating. It must be checkable: "`node --test test/split.test.js` passes and covers 1000 / 3" |
| Never ask, never wait | a member ending on a question nobody will answer |
| Word limit | reports flooding the lead's context |

Then add only the repo facts the member needs (the test command, the commit format, the repo's hard rules) and a usage stop line, once, if there is one. Ask for output in the shape you'll consume: scouts give ranked findings with the exact change; builders give their commits, the checks they ran, "Outside my files", and what's left undone; reviewers give severity, file:line, the failure, and the fix.

**A bad brief:** "Fix the bugs we found in the money code, and clean up whatever else you see. Let me know if anything's unclear." "We found" is context the builder doesn't have, "the money code" names no files, "whatever else" invites edits outside its files, and "let me know" invites a question nobody will answer.

**Rubric:** 1 goal in one line · 2 the piece, named exactly · 3 what the others cover · 4 builders: lane, branch, files owned, no file owned twice · 5 a checkable done line · 6 the never-ask line · 7 a word limit · 8 the repo facts it needs and nothing from the conversation · 9 nothing personal or secret.

## Guide for the agent

1. Rebuild the dojo with its pretend board: `node ~/.claude/skills/swarm-school/labs/seed-dojo.mjs ~/swarm-dojo --reset --board`. Have the learner read `BOARD.md` (issues #1 to #7) and list the files (`git -C ~/swarm-dojo ls-files`).
2. Have the learner write, in one message: a roster line; an ownership table for two builders plus the lead (files each owns, issues landing in each lane); what the lead does itself (hint: #7 is a product call, and someone has to own `README.md` and `CHANGELOG.md`); and both builder briefs.
   Checkpoint: grade the split against "The build lab's file split" in `dojo-answer-key.md`. If they split by issue count, show the collision (#3 and #5 both edit `store.js`). Grade each brief against the rubric, explaining every miss by the failure it would cause.
3. Have the learner fix what the grading found, then save the final briefs to `~/swarm-dojo-briefs.md`, outside the dojo, so story 13.6 can use them and `--reset` won't erase them.
4. Three quick ones, one at a time:
   Checkpoint: two scouts return the same five findings. What was wrong with the plan? (Overlapping angles, or no "the others cover".)
   Checkpoint: two builders both need a new `Money` type. How do you avoid a conflict? (Seam first: the lead commits the type, then cuts the lanes.)
   Checkpoint: "Done when: it works." What's wrong with it? (It isn't checkable. Name the command and what it must cover.)

Point out when it comes up:

- If #7 goes the "implement `--currency`" way, that code lands in `cli.js`, which a lane owns. The product call is the lead's; the code belongs in that lane's brief.

## Done when

- [ ] An ownership table with no file owned twice and hot files assigned
- [ ] Two builder briefs that pass the rubric
- [ ] Briefs saved to `~/swarm-dojo-briefs.md`

## Log prompt

What did your first split look like, and what collision did grading catch?
