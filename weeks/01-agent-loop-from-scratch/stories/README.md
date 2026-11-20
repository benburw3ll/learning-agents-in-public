# Week 01 stories

Run them in order. Each takes one to two hours. In a Claude Code session in this repo, say "run story 1.N" and it will tutor you through it (the rules are in the repo's CLAUDE.md).

## Defaults for this week

- Language: TypeScript with `@anthropic-ai/sdk`, since most of your repos are TypeScript. Python works the same way if you'd rather.
- Target repo for the real task: `widgethub` (public), or any repo of yours with a test suite.
- Model: `claude-opus-5-5`. Use a cheaper model while iterating on the loop if you want; switch back for the real task.
- A fresh repository for the loop itself, for example `agent-loop`.

## Prerequisites

- An Anthropic API key with a few dollars of credit. The Max subscription covers Claude Code, not raw API calls. Set it in your shell, never in a file in the repo.
- Node 20 or newer.
- For story 1.8 only: OpenAI API credit, which ChatGPT Plus does not include.

## The stories

| # | Story | Afterward you can explain |
|---|-------|---------------------------|
| 1.1 | [One call, one tool](01-one-call-one-tool.md) | What a tool_use block is, and who actually runs the tool |
| 1.2 | [The loop](02-the-loop.md) | Why an agent is a while loop over stop_reason |
| 1.3 | [Edit tool and a real task](03-edit-tool-and-a-real-task.md) | How tool design shapes behavior |
| 1.4 | [The permission gate](04-the-permission-gate.md) | Where Claude Code's permission modes live in the loop |
| 1.5 | [Context and compaction](05-context-and-compaction.md) | Why context management is the hard part |
| 1.6 | [System prompt and caching](06-system-prompt-and-caching.md) | What CLAUDE.md actually is, and why prefix order matters |
| 1.7 | [Rebuild on the Agent SDK](07-rebuild-on-the-agent-sdk.md) | What the SDK gives you for free, and what it hides |
| 1.8 | [Stretch: streaming and a second provider](08-stretch-streaming-and-a-second-provider.md) | Where the two vendors' APIs differ in tool-call shape |
