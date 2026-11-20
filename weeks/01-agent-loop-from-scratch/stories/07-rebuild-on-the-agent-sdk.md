# Story 1.7: Rebuild on the Agent SDK

Time: two hours. Prerequisite: story 1.6.

## Goal

Do story 1.3's real task again, this time with the Claude Agent SDK. Compare lines of code, what came for free, and what got hidden.

## Afterward you can explain

- What the SDK provides: built-in tools, permissions, hooks, compaction, subagents, sessions
- Where each piece of your own loop maps onto an SDK option
- When you'd choose raw API, the SDK, or the CLI

## Guide for the agent

1. Have the learner install the Agent SDK and run the smallest possible query against the target repo with the same task as story 1.3.
2. Map each thing they built in stories 1.1 to 1.6 onto an SDK feature: tools onto built-in Read, Edit, Bash; the gate onto permission modes and hooks; compaction onto the automatic kind; the instructions file onto CLAUDE.md and system prompt options; the audit log onto hooks.
   Checkpoint: which of their pieces has no SDK equivalent? Which SDK features have no equivalent in their loop?
3. Have them implement one PreToolUse hook that reproduces their deny-list.
4. Have them add one custom tool through an in-process MCP server, so they see how custom tools enter the SDK.
5. Have them write the comparison in the agent-loop repo's README: lines of code, features, what the SDK hides, and whether that matters.

Point out when it comes up:

- The SDK is Claude Code as a library. The Tool Runner in the base SDK is a different, smaller thing.
- Hiding the loop is the point, and also the cost. Knowing both is why this week exists.

## Done when

- [ ] The same task completed through the SDK
- [ ] The deny-list reproduced as a hook
- [ ] One custom tool added over MCP
- [ ] The comparison README written

## Log prompt

Would you ship your own loop anywhere? Where, and why not elsewhere?

## Resources

- Claude Agent SDK: https://code.claude.com/docs/en/agent-sdk
