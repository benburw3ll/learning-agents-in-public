# Week 01: Agent loop from scratch

Track: Under the hood

## Goal

Write a minimal coding agent against the raw Claude API in a few hundred lines: a tool-calling loop, a bash tool, a file-edit tool, a permission gate, and naive context compaction. Then rebuild the same agent on the Claude Agent SDK and write down what the SDK gave for free.

## Why it matters

Every feature in Claude Code and Codex is a hook on one step of this loop. Once I've written the loop myself, new features stop being magic and start being "oh, that's a hook on the tool-result step". It also makes the two tools' differences legible.

## Deliverable

A separate repository with two implementations and a README comparing them, linked from this week's log.

## Stories

Guided, in order, in [stories/](stories/README.md). Say "run story 1.1" to a Claude Code session in this repo to start.

## Done when

- [ ] The raw-API agent can read, edit, and run tests in a real repo of mine
- [ ] A permission gate blocks destructive commands and asks before running them
- [ ] Compaction triggers at a token threshold and the agent keeps working afterwards
- [ ] The same task is completed on the Agent SDK, with a write-up of what came for free
- [ ] Both versions handle parallel tool calls correctly (all results returned in one turn)

## Stretch

- Streaming with eager tool-input streaming
- Run the same loop against the OpenAI Responses API and note the differences in tool-call shape
- Add a tiny memory tool and see how the agent uses it

## Resources

- Claude API docs: https://platform.claude.com/docs
- Claude Agent SDK: https://code.claude.com/docs/en/agent-sdk
- Anthropic, "Building effective agents": https://www.anthropic.com/engineering/building-effective-agents
- Codex repository: https://github.com/openai/codex
