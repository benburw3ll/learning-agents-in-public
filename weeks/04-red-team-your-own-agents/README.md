# Week 04: Red-team your own agents

Track: Under the hood

## Goal

Plant instructions in a README, an issue, a web page, and a tool result, then watch what each tool does with them. Then learn the containment: sandbox modes, devcontainers, network allowlists, and permission modes.

## Why it matters

Prompt injection is what separates people who run agents on real systems from people who get burned. Knowing exactly how my setup fails is worth more than any amount of reading about it.

## Deliverable

A documented set of injection attempts with what each tool did, and a sandboxed configuration I trust enough to run unattended.

## Done when

- [ ] Five injection attempts documented, with the outcome in each tool
- [ ] Claude Code sandbox and Codex sandbox configured and compared
- [ ] A devcontainer with a network allowlist that agents run inside
- [ ] A one-page threat model for my own setup
- [ ] At least one surprising failure found and a mitigation written down

## Stretch

- A hook that flags injection-shaped text in tool output
- Test whether a malicious MCP server can steer the agent, and what limits it

## Resources

- Claude Code security: https://code.claude.com/docs/en/security
- Claude Code sandboxing: https://code.claude.com/docs/en/sandboxing
- Dev containers: https://containers.dev
- Codex docs: https://developers.openai.com/codex
