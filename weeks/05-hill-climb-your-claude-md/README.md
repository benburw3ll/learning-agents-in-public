# Week 05: Hill-climb your CLAUDE.md

Track: Measure

## Goal

Build a small eval set for my own instructions and skills, with a held-out test split, and hill-climb my CLAUDE.md and one skill against it.

## Why it matters

Most people edit prompts by feel and never find out whether the edit helped. Measuring is the whole difference between a config that drifts and one that improves.

## Deliverable

An eval set, a baseline score, and three rounds of changes that were each kept or reverted on data.

## Done when

- [ ] Twenty or more eval cases with a written grading method
- [ ] Baseline score recorded before any change
- [ ] Three rounds of changes, each kept or reverted based on the held-out score
- [ ] Skill triggering accuracy measured before and after
- [ ] A short note on what kind of instruction moved the score and what didn't

## Stretch

- Run the same eval set against Codex with an equivalent AGENTS.md
- Automate the eval run so it can be re-run in one command

## Resources

- Claude Code memory and CLAUDE.md: https://code.claude.com/docs/en/memory
- Agent skills: https://code.claude.com/docs/en/skills
- Anthropic, "Claude Code best practices": https://www.anthropic.com/engineering/claude-code-best-practices
