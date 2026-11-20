# Story 1.1: One call, one tool

Time: about an hour. Prerequisites: API key set in your shell, Node 20+, an empty `agent-loop` repo.

## Goal

Make one Messages API call with a single `bash` tool declared. See the model ask to use it. Run the command yourself, by hand. Send the result back. Watch the model finish.

## Afterward you can explain

- What is in a request: model, max_tokens, system, messages, tools
- What a `tool_use` content block is, and that the model never runs anything; your code does
- What `stop_reason` tells you

## Guide for the agent

Tutor mode. The learner writes the code.

1. Ask the learner to say, in one sentence, who executes a tool when Claude "uses" one. Don't correct it yet. Come back to it at the end.
2. Have them create the repo, run `npm init -y`, install `@anthropic-ai/sdk`, and confirm `ANTHROPIC_API_KEY` is set in the shell and not in any file.
3. Have them write a script that calls `client.messages.create` with model `claude-opus-5-5`, `max_tokens: 16000`, one user message ("What files are in the current directory?"), and a `tools` array with one custom tool named `bash` whose input schema has a single `command` string. Point them at the tool-use docs rather than dictating the schema.
   Checkpoint: before they run it, ask them to predict the `stop_reason` and what the `content` array will hold.
4. Run it. Have them print `response.content` as JSON and find the `tool_use` block: its `id`, `name`, `input`.
5. Have them run the command by hand in their terminal. Then build a second request: the original messages, plus the assistant's full `content` as an assistant message, plus a user message holding one `tool_result` block with the `tool_use_id` and the output as text.
   Checkpoint: ask why the assistant content must go back whole, not just its text.
6. Run it. The model should answer in prose with `stop_reason` of `end_turn`.
7. Return to the question from step 1. Have them rewrite their sentence.

Point out when it comes up:

- The model never executes anything. A "tool" is a promise your code keeps.
- Tool inputs arrive as parsed JSON. Never string-match the serialized form.
- Thinking is on by default on current models. Nothing to configure for this story.

## Done when

- [ ] A script makes the first call and prints the `tool_use` block
- [ ] A second call returns the `tool_result` and the model answers in prose
- [ ] The learner can state who runs the tool without looking

## Log prompt

Three lines in LOG.md: what you expected the first response to look like, what it actually looked like, and the one thing that surprised you.

## Resources

- Tool use: https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview
- Messages API reference: https://platform.claude.com/docs/en/api/messages
