# Story 1.4: The permission gate

Time: one to two hours. Prerequisite: story 1.3.

## Goal

Put a gate between the model's tool call and its execution: auto-allow safe commands, ask on risky ones, hard-deny a few. Log every call.

## Afterward you can explain

- Where Claude Code's permission modes live in the loop
- Why the gate has to be code, not a sentence in the prompt
- The difference between asking, denying, and sandboxing

## Guide for the agent

1. Open with a question: if the system prompt says "never run rm -rf", is that a security control? Let the learner argue it out. Move on without settling it.
2. Have them write a classifier: an allow-list of read-only commands (ls, cat, grep, git status, the test runner), a deny-list (rm -rf, git push --force, curl piped to sh, anything under ~/.ssh), and everything else asks for y/n on the terminal. The deny and ask steps run in code before the tool function does.
3. Have them test each path with a prompt designed to trigger it ("clean up the build directory").
   Checkpoint: what does the model do when a call is denied? Have them return a `tool_result` with `is_error: true` that explains the denial, and watch.
4. Add an audit log: one JSON line per tool call with timestamp, tool, input, decision, and duration.
5. Add a plan-mode flag: when set, only read-only tools appear in the `tools` array at all. Compare removing tools against denying them at the gate. Which does the model handle better?
6. Map what they built onto Claude Code: default mode, plan mode, auto mode, bypass, and hooks as the extension point. Have them say where each sits in their loop.

Point out when it comes up:

- A prompt instruction is a preference. The gate is a control. A sandbox is a boundary. All three matter; only two are enforceable.
- Return to the step 1 question here.

## Done when

- [ ] Allow, ask, and deny paths each demonstrated
- [ ] Audit log written per call
- [ ] Plan mode implemented by restricting the tool list
- [ ] The learner can map Claude Code's permission modes onto their loop

## Log prompt

Which deny-list entry would you be embarrassed to have missed? Add it, and write down why you missed it.

## Resources

- Claude Code permissions: https://code.claude.com/docs/en/permissions
- Claude Code hooks: https://code.claude.com/docs/en/hooks
