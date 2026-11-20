# Week 03: Mod the tools

Track: Under the hood

## Goal

Package my hooks, skills, status line, and MCP config as a Claude Code plugin with its own marketplace, and the equivalent Codex plugin. One command should set up a fresh machine the way I like it.

## Why it matters

Plugins are how expertise gets shared. If my setup only lives in my home directory, nobody else can use it, including future me on a new laptop.

## Deliverable

Two installable plugins from marketplaces I own, plus an eval suite that proves at least one skill triggers correctly.

## Done when

- [ ] A Claude Code plugin installs from my own marketplace
- [ ] A Codex plugin installs from a marketplace too
- [ ] A PreToolUse hook that blocks a destructive command is covered by a test
- [ ] A plugin eval suite passes for at least one skill
- [ ] A fresh user account on this machine goes from zero to my setup in one command

## Stretch

- A pane or status-line mod that shows something I actually care about during a session
- A hook that runs the project's formatter after every edit

## Resources

- Claude Code plugins: https://code.claude.com/docs/en/plugins
- Claude Code hooks: https://code.claude.com/docs/en/hooks
- Agent skills: https://code.claude.com/docs/en/skills
- Codex docs: https://developers.openai.com/codex
