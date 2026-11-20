# Week 13: Agent swarms

Track: Bonus

## Goal

Understand agent swarms well enough to plan one on paper, run it to a single PR, and say afterwards whether it was worth the tokens. A swarm here means one lead session plus a few subagents, each with one brief and one report back.

## Why it matters

"A team of agents working together" is easy to say and easy to get wrong: agents doing the same work twice, builders overwriting each other's files, a PR per agent, a lead drowning in reports. Launching agents is the easy part. The skill is splitting the work so pieces don't collide, writing briefs a cold agent can finish without asking, and bringing it all back together once.

## Deliverable

- Stories 13.1 to 13.7 done, with labs run on a practice repo that has ten planted bugs and a test suite that passes anyway.
- One real swarm on one of my own repos, planned on paper first, landed as one PR, and debriefed in LOG.md.
- My swarm kit (the skill, the three member roles, the lane scripts and the practice repo) published as its own repository and linked from LOG.md.

## Stories

In [`stories/`](stories/README.md), in order. In a Claude Code session in this repo, say "run story 13.N".

## Done when

- [ ] Stories 13.1 to 13.7 done, each one's checkpoints answered
- [ ] The QA lab (13.3) found at least 6 of the dojo's 10 planted bugs
- [ ] The dojo build swarm (13.6) gathered into one branch without a conflict, and the full test suite passed once after gathering
- [ ] A gather conflict resolved on purpose, with gather finishing cleanly afterwards
- [ ] A real swarm on one of my repos landed as one PR (13.8)
- [ ] The swarm kit is public in its own repository and installs on a fresh machine
- [ ] LOG.md says what the real swarm cost and whether doing it inline would have been cheaper

## Stretch

- Package the swarm kit as a Claude Code plugin (week 3's territory)
- Run the same QA job inline and as a three-scout swarm, and compare tokens, time and findings
- Write a preset of my own, with the brief lines that made it work

## Resources

- Claude Code subagents: https://code.claude.com/docs/en/sub-agents
- Git worktrees: https://git-scm.com/docs/git-worktree
- Git cherry-pick: https://git-scm.com/docs/git-cherry-pick
