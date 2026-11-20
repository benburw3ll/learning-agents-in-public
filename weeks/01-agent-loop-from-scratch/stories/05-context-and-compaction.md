# Story 1.5: Context and compaction

Time: two hours. Prerequisite: story 1.4.

## Goal

Watch the context grow until it becomes the problem, then handle it: track usage per turn, clear or summarize old history past a threshold, and keep the agent working through a long task.

## Afterward you can explain

- Why context management is the hard part of an agent
- The difference between clearing old tool results and summarizing history
- What Claude Code's auto-compaction is doing when it fires

## Guide for the agent

1. Have the learner give the agent a deliberately long task on the target repo ("summarize what every file under src does"). Have them table `input_tokens` per turn from their log.
   Checkpoint: at which turn would this hit a context limit, and what does a single turn cost by then?
2. Strategy one, clearing. Replace the content of tool results older than N turns with a short placeholder. Rerun. Does the agent still finish? What breaks?
3. Strategy two, summarizing. When input tokens pass a threshold, make a separate call asking the model to summarize the conversation so far into a compact note, then restart the messages array from that note. Rerun.
   Checkpoint: what information got lost in the summary? Have them compare behavior before and after.
4. Compare with the API's own option: read about server-side compaction in the docs and try it if they want. Note that compaction blocks have to be sent back whole, not reduced to text.
5. Discuss when each fits: clearing for noisy tool output, summarizing for long sessions, and what a memory file adds on top.

Point out when it comes up:

- Thinking blocks and compaction blocks go back unchanged on current models.
- Once the loop can lose information, the agent needs a way to find it again. That is what grep and memory tools are for.

## Done when

- [ ] Per-turn token table for a long task
- [ ] Tool-result clearing implemented and evaluated
- [ ] Summarization implemented and evaluated
- [ ] A paragraph on what each strategy lost

## Log prompt

At what point did the agent start getting worse, and how did you notice?

## Resources

- Context windows: https://platform.claude.com/docs/en/build-with-claude/context-windows
- Anthropic, "Effective context engineering for AI agents": https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
