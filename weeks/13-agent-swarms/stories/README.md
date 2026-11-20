# Week 13 stories

Run them in order. Stories 13.2, 13.4 and 13.7 are drills with no agents, about half an hour each. The others launch real subagents against a practice repo. In a Claude Code session in this repo, say "run story 13.N" and it will tutor you through it (the rules are in the repo's CLAUDE.md).

In the labs you are the lead: you write the roster, the split and the briefs, and the session launches the members you briefed. It never writes a brief for you unless you ask after trying.

## Defaults for this week

- The practice repo ("the dojo"): `~/swarm-dojo`, a tiny bill-splitting CLI called potluck with ten planted bugs and eight tests that pass anyway. `seed-dojo.mjs` builds it and rebuilds it with `--reset`. Its `origin` is a bare repo in a local folder, so "pushing" never leaves the machine.
- Lab members run on Sonnet. The builder role's default (Opus at extra-high effort) is for real work; overriding the model to fit the job is part of the lesson.
- No more than four members in any lab.
- The kit: install it from [swarm-kit](https://github.com/benburw3ll/swarm-kit). Run `git clone https://github.com/benburw3ll/swarm-kit.git`, then `node install.mjs` inside the clone. That puts the swarm skill in `~/.claude/skills/swarm/`, the member roles in `~/.claude/agents/` (`swarm-scout.md`, `swarm-builder.md`, `swarm-reviewer.md`) and the course with its lab scripts in `~/.claude/skills/swarm-school/` (the scripts in `labs/`). It won't overwrite files that are already there unless you pass `--force`. Start a new session afterwards so the roles load.

## Prerequisites

- Claude Code (desktop app or CLI). Subagents ship with it.
- Git 2.40 or newer and Node 20 or newer. On Windows, run the shell scripts from Git Bash.
- The swarm kit installed under `~/.claude` (see above). A session started before the role files existed won't see them; start a new one.

## The stories

| # | Story | Afterward you can explain |
|---|-------|---------------------------|
| 13.1 | [What a swarm is](01-what-a-swarm-is.md) | Why a swarm is a hub, not a group chat, and why the brief is the member's whole world |
| 13.2 | [Roles, models and cost](02-roles-models-and-cost.md) | Which role and model each member gets, and when a swarm is the wrong tool |
| 13.3 | [The lifecycle and the one-PR rule](03-the-lifecycle.md) | Every step from clearing the field to the report, and why each "once" rule exists |
| 13.4 | [The common swarms](04-the-common-swarms.md) | The six presets, how each one gathers, and how to chain them |
| 13.5 | [Splitting the work and writing briefs](05-splitting-and-briefs.md) | Orthogonal angles, disjoint files, hot files, seams, and a brief a cold agent can finish |
| 13.6 | [Lanes, gather and conflicts](06-lanes-and-gather.md) | How worktree lanes come back as one branch, and what to do when they collide |
| 13.7 | [Techniques and anti-patterns](07-techniques-and-anti-patterns.md) | Twelve techniques, and how to spot a broken plan before it spends anything |
| 13.8 | [Capstone: a real swarm](08-capstone.md) | Whether a swarm on real work earned its tokens |

[`dojo-answer-key.md`](dojo-answer-key.md) lists the planted bugs, how to score a lab, and the reference fixes. It is for the tutor and for after a lab; never put it in a member's brief.
