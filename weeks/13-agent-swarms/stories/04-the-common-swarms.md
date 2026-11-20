# Story 13.4: The common swarms

Time: about 30 minutes. Prerequisite: story 13.3. A drill: no agents.

## Goal

Hear an ask and name the preset and roster in one line, and chain presets for jobs too big for one.

## Afterward you can explain

- The six presets, their default rosters, and how each one comes back together
- Why readers split by angle and writers split by files
- How a bigger job becomes a short chain of presets that still ends in one PR

## Key ideas

| Preset | Default roster | You'd say | How it comes back |
| --- | --- | --- | --- |
| **qa** | 4 scouts, Opus | "audit", "QA team", "give me recommendations" | the lead applies the safe recommendations in one branch and PR (user-level config directly) and lists what it skipped |
| **build** | 3 builders + 1 reviewer | "build these", "knock out the batch" | gather, run the suite once, reviewer, fixes on the same branch, one PR with a `Closes #n` per issue |
| **ui-pass** | 4 builders by screen area + 1 reviewer | "pass over the screens", "polish the pages" | as build; each lane runs its own dev server on its own port and data folder |
| **review** | 3 reviewers, Opus | "second opinion on the branch" | fixes on the same branch; no new PR |
| **plan** | 3 scouts | "plan this out", "file issues for" | issue drafts as text; the lead files them all in one batch |
| **research** | 3 scouts, Sonnet | "look into", "compare options" | the lead writes the answer; nothing committed unless asked |

What makes each work:

- **qa:** four angles that don't overlap. For code: correctness; rules and security; tests and fixtures; words and states in the UI. For an agent workflow: the PR and CI pipeline; the skills and rules; transcripts (what was asked, where time went); what loads where.
- **build:** a split by files, not by issue count. A small script that groups issues by the files they touch saves most of the thinking.
- **ui-pass:** screen areas that map to folders, and shared styles with exactly one owner.
- **review:** one angle per reviewer: correctness; the repo's rules and security; simplification and dead code. A security reviewer only for risky paths (secrets, auth, AI calls, anything that touches a real machine).
- **plan:** scouts draft, never file, so the board changes once, in one consistent shape.
- **research:** one question per scout. "Research everything about X" is not a question.

Chains for bigger jobs, still one branch and one PR:

| Job | Chain |
| --- | --- |
| Find what's wrong and fix it | qa → the lead triages (small fixes applied directly) → build for the rest → reviewer → one PR |
| Plan the next milestone | research → the lead decides → plan → one batch of issues |
| A feature across the app | two Sonnet scouts map where it touches → the lead writes the file split and lands the shared interface → build |

The shape isn't only for code: anything that splits into owned pieces works (applying a theme across many settings, say), with the same rules: disjoint ownership, one lead, one gather, a way back.

## Guide for the agent

1. Give the learner all ten asks in one message. For each, a one-line roster ("build: 2 builders (web, cli) + 1 reviewer") or "not a swarm: …".
   1. Go over the onboarding screens and make them read better.
   2. Why is CI so slow?
   3. Knock out the six issues in this milestone.
   4. Second opinion on this branch before I merge.
   5. What are our options for syncing with a fitness watch?
   6. Turn this design doc into issues.
   7. Fix the typo in the README.
   8. Work the board while I sleep.
   9. Audit my Claude Code skills for contradictions.
   10. Add dark mode to the web app and the admin console.
   Checkpoint: grade. Expected: ui-pass; qa or research (pipeline timings, runner health, workflow config); build grouped by files plus a reviewer; review; research, one scout per option; plan; not a swarm (inline); not a swarm (an unattended run); qa on user-level config, no PR; build or ui-pass with two lanes and the shared theme owned by one lane or landed first by the lead.
2. Have the learner pick a real job from one of their own boards and write the chain they'd use, with one roster line per link.
   Checkpoint: is every link needed? Where does the lead decide between links? Does it still end in one PR?
3. Checkpoint: which presets end with no commits by default, and why do plan scouts draft instead of filing? (research, and plan, whose output is filed issues; drafting keeps the board changing once.)

Point out when it comes up:

- Saying the roster in one line before launching is the cheapest check there is. If you can't say it, the split isn't ready.

## Done when

- [ ] The ten asks graded, with at least eight right
- [ ] One chain written for a real job of yours
- [ ] You can say the six presets and how each gathers

## Log prompt

Which preset do you expect to use most, and which one surprised you?
