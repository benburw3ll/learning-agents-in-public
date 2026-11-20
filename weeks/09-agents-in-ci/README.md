# Week 09: Agents in CI

Track: GitHub deep end

## Goal

Run the official Claude Code GitHub Action and Codex in CI on my own repos: PR review, issue triage, "explain this failure". Tune the noise down until I would actually keep them on.

## Why it matters

Agents in CI are the version of this that scales past one person. The hard part isn't turning them on, it's making them worth reading.

## Deliverable

Two repos with agent review turned on, plus a headless job that produces an artifact, and a signal-to-noise write-up.

## Done when

- [ ] The Claude Code action reviews PRs on one repo
- [ ] Codex reviews PRs on one repo, via cloud review or CI
- [ ] A headless job (non-interactive Claude or Codex) produces an artifact on a schedule
- [ ] A write-up of what I turned off and why
- [ ] Review comments that were wrong are counted, not just the ones that were right

## Stretch

- An action that fixes failing CI and opens a PR
- A triage bot that labels new issues and asks for missing details

## Resources

- Claude Code GitHub Actions: https://code.claude.com/docs/en/github-actions
- claude-code-action: https://github.com/anthropics/claude-code-action
- Codex docs: https://developers.openai.com/codex
