# Story 1.6: System prompt and caching

Time: one to two hours. Prerequisite: story 1.5.

## Goal

Give the agent a project instructions file (its own CLAUDE.md), see behavior change, then cache the stable prefix and prove the cache is hitting.

## Afterward you can explain

- What CLAUDE.md actually is (text in the system prompt) and what it isn't (a rule engine)
- Why prefix order matters for caching
- How to tell whether caching is working at all

## Guide for the agent

1. Have the learner write a short instructions file for the target repo: the test command, two style rules, one "always do X". Load it into the system prompt and rerun story 1.3's task.
   Checkpoint: which instructions did the model follow, which did it skip, and how can they tell?
2. Add `cache_control` to the system prompt and the tool definitions. Run two identical requests. Have them read `usage.cache_read_input_tokens` on the second.
3. Break it on purpose: put a timestamp at the top of the system prompt. Rerun. Cache reads drop to zero. Move the timestamp to the end of the last user message. Rerun.
   Checkpoint: write the ordering rule in one sentence (tools, then system, then messages; stable first, volatile last).
4. Measure: run the long task from story 1.5 with and without caching and compare the cost from `usage`.
5. Discuss what this means for Claude Code: why CLAUDE.md loads once, why skills load lazily, why a changing status line inside the prompt would be expensive.

Point out when it comes up:

- A short prefix below the minimum size silently doesn't cache. Check the number, don't assume.
- Cache hits are the first lever for cost, before model choice.

## Done when

- [ ] The instructions file changes behavior, with evidence
- [ ] Cache reads confirmed non-zero on a repeated request
- [ ] The timestamp experiment logged
- [ ] Cost compared with and without caching

## Log prompt

One instruction the model ignored, and your best guess why.

## Resources

- Prompt caching: https://platform.claude.com/docs/en/build-with-claude/prompt-caching
- Claude Code memory: https://code.claude.com/docs/en/memory
