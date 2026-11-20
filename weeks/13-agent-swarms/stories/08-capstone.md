# Story 13.8: Capstone, a real swarm

Time: about an hour plus the swarm's run time. Prerequisite: stories 13.1 to 13.7.

## Goal

Plan a swarm on real work in one of your own repos, defend each choice, run it to one PR, and judge afterwards whether it was worth the tokens.

## Afterward you can explain

- Why each member was in the roster, and what each one cost against what it returned
- Where the plan met reality: conflicts, overlap, a member that wandered, a suite failure after gathering
- Whether inline would have been faster or cheaper

## Guide for the agent

This is the one story that leaves the dojo. It opens a real branch and a real PR, so it runs only after the learner says go.

1. The learner picks a real job: two to four small issues that touch different folders (build); an audit of one skill folder or one plugin (qa); an open question that needs options compared (research); a pass over two or three screens (ui-pass).
   Checkpoint: is it big enough to need two to four members and small enough to finish in one sitting? If inline is the right answer, say so: choosing not to swarm is a pass.
2. In that repo, run `bash ~/.claude/skills/swarm/scripts/busy.sh` and show the learner the files other work already holds.
3. The learner writes the whole plan in one message: the ask in one line; preset and roster line; the split (angles, or an ownership table with hot files and their one owner, and any seam the lead lands first), avoiding held files; the briefs; the lead's share; the full suite command, the reviewer's angle and the PR's done line; a cost guess (members × model) and why this beats doing it inline.
   Checkpoint: grade the plan against 13.5's rubric and 13.7's anti-pattern table. For every problem, name the failure it would cause and the fix. Be blunt about cost.
4. After the learner fixes the plan and says go, run it through the swarm skill's steps: one branch, one PR, merge on green in the background. Narrate each step in one line as it happens ("lanes cut: web, cli", "gathered 5 commits, suite green").
5. Debrief together.
   Checkpoint: which member's report earned its tokens? Which didn't? What would you change in the briefs or the split next time? Would inline have been faster or cheaper?
6. If the debrief shows a change to the swarm skill, a preset or a role file that would have helped, the learner makes it in their kit and notes it in LOG.md.

## Done when

- [ ] A written plan, graded and fixed before anything launched
- [ ] The swarm landed as one PR
- [ ] The debrief questions answered in LOG.md, including the cost and the inline comparison

## Log prompt

The honest one: was this swarm worth it? What's the smallest job you'd swarm now?
