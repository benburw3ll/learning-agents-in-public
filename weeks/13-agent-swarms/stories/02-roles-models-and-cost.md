# Story 13.2: Roles, models and cost

Time: about 25 minutes. Prerequisite: story 13.1. A drill: no agents.

## Goal

Know which role and model each member gets, estimate what a swarm costs before launching it, and recognise when a swarm is the wrong tool.

## Afterward you can explain

- What the lead, scout, builder, reviewer and housekeeper each own
- How to pick a member's model by what a miss would cost
- When to use inline work, one subagent, a swarm, a separate session or an unattended run instead

## Key ideas

| Part | Writes? | Default model | Job |
| --- | --- | --- | --- |
| Lead (your session) | the swarm's branch | the session's | split the work, write briefs, do its own share, gather, run the gate, open the one PR, make the calls |
| `swarm-scout` | no | Sonnet | read, audit, research; a ranked report with exact changes |
| `swarm-builder` | only in its own lane | Opus, extra-high effort | build one piece in its own worktree, commit there, never push |
| `swarm-reviewer` | no | Opus, high effort | review the gathered branch from one angle; only findings worth fixing |
| Housekeeper | mechanical only | Haiku | after the merge: remove worktrees, tick boxes |

- **Role files** hold the rules every member of a role follows (read-only, never ask, never push). The brief then carries only what's specific to the job. A session started before a role file existed can't see it: use a general-purpose subagent and paste the role's rules into the brief.
- **Models by the cost of a miss:** reading volume → Sonnet; judgement the lead will apply without re-checking → Opus; writing code → Opus; a scripted checklist → Haiku; the top model only where a miss is costly, with the reason said out loud.
- **Cost, roughly:** (members × what each one reads) + what the lead reads back. Levers, cheapest first: fewer members, narrower pieces, word limits on reports, Sonnet for reading, and doing things once.
- **Swarm or something else:**

| Situation | Use |
| --- | --- |
| One small change you can see | inline |
| One big search whose details you don't need | one subagent |
| 2–5 independent pieces, results needed this turn | a swarm |
| A separate task you'll steer yourself, landing as its own PR | a new session |
| Working through an issue board for hours while you're away | an unattended run |

A subagent lives inside the turn and returns one report (the lead can continue it with SendMessage). A session is a whole conversation: it shows in the sidebar, keeps its own context, outlives the turn, and you can talk to it.

## Guide for the agent

1. Have the learner open the three role files in `~/.claude/agents/` and list the rules they share.
   Checkpoint: which of those rules never need to appear in a brief, and why? (All of them: the role file already carries them.)
2. Give the learner these eight situations in one message. For each they answer: inline, one subagent, swarm (which roles), session, or unattended run.
   1. Rename a helper function everywhere.
   2. "Where does the app read its config? I just need the answer."
   3. Audit my Claude Code skills for contradictions and bloat.
   4. Build four issues that touch the web app, the CLI and two plugins.
   5. Keep working through the board tonight.
   6. Draft a design doc I want to steer over the next day.
   7. Compare three libraries for parsing dates.
   8. Fix the one failing test in CI.
   Checkpoint: grade them. Expected: inline; one subagent; swarm (scouts on separate angles); swarm (builders split by files, plus a reviewer); unattended run; session; swarm (one Sonnet scout per library); inline.
3. Have the learner estimate a four-scout audit against one agent doing the same audit alone.
   Checkpoint: why is the swarm never cheaper in tokens, and what does it buy instead?
4. Checkpoint: when does a scout get Opus instead of Sonnet? (When its output is judgement the lead will apply without re-checking.)

Point out when it comes up:

- The labs override builders to Sonnet because the dojo's fixes are tiny. Fitting the model to the work is a real technique, not a lab shortcut.

## Done when

- [ ] The eight situations graded, with at least six right
- [ ] You can say the five parts and each one's default model
- [ ] You can name three levers that cut a swarm's cost

## Log prompt

Which of the eight situations would you have swarmed a month ago that you now wouldn't?
