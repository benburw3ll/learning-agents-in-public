# Story 1.2: The loop

Time: one to two hours. Prerequisite: story 1.1.

## Goal

Turn the two hand-made calls into a loop: while `stop_reason` is `tool_use`, run every tool call, send all the results back in one user message, repeat. Handle failures and parallel calls.

## Afterward you can explain

- An agent is a loop over `stop_reason` plus a dispatch table of tools
- Why every tool result from one assistant turn goes back in a single user message
- What `is_error` on a tool result does

## Guide for the agent

1. Ask the learner to sketch the loop as pseudocode in a comment before writing it.
   Checkpoint: review the sketch. Where does the loop exit? What happens on `max_tokens`?
2. Have them implement it: a map from tool name to async function; for each `tool_use` block, run the function and collect a `tool_result`; push one user message holding all of them.
3. Have them give the model a task that needs several commands ("find the largest file in this repo and tell me its line count"). Have them log each iteration: `stop_reason`, tool names, and `usage.input_tokens` / `usage.output_tokens`.
4. Force a failure (a command that doesn't exist). Have them return the stderr with `is_error: true` and watch the model recover.
   Checkpoint: what would happen if they dropped the failed result instead of returning it?
5. Parallel calls. Ask for two independent things in one prompt ("count the lines in README.md and list the top-level directories"). The assistant message may hold two `tool_use` blocks. Have them run the tools concurrently and confirm both results return in one user message.
6. Add an iteration cap, and handle `stop_reason` values other than `tool_use` and `end_turn` (`max_tokens`, `refusal`) by printing them and exiting cleanly.

Point out when it comes up:

- Splitting parallel results across several messages quietly teaches the model to stop calling tools in parallel.
- `usage` is how context growth gets tracked in story 1.5. Log it from day one.

## Done when

- [ ] A multi-step task completes through the loop
- [ ] A failed tool returns `is_error` and the model recovers
- [ ] Parallel tool calls run concurrently and return in one message
- [ ] Other stop reasons are handled, and there is an iteration cap

## Log prompt

How many lines is the loop itself? Write the number down, next to what you guessed it would be before this week.

## Resources

- Tool use, including parallel calls and errors: https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview
