# Story 1.8: Stretch, streaming and a second provider

Time: two hours. Prerequisite: story 1.2 at least. Needs OpenAI API credit for the second half.

## Goal

Stream the loop so output appears as it is generated, then port the loop to the OpenAI Responses API and write down where the two differ.

## Afterward you can explain

- What changes in the loop when responses stream
- Where the two vendors' APIs differ in tool-call shape and result handling

## Guide for the agent

1. Have the learner switch to the streaming call, print text as it arrives, and use the SDK's final-message helper to get the complete response for the loop. Turn on eager input streaming for their client tools and validate each parsed input against its schema before running it, since the API no longer guarantees it.
   Checkpoint: what can now arrive incomplete, and how does their code notice?
2. Have them port the loop from story 1.2 to the OpenAI Responses API and run the same multi-step task.
3. Have them write a short table of differences: how a function call is represented, how results are returned, how reasoning is handled, how parallel calls look.

## Done when

- [ ] Streaming works with the loop intact
- [ ] The second-provider loop completes story 1.2's task
- [ ] The differences table is in the agent-loop README

## Log prompt

Which difference would bite you first if you switched providers on a real project?

## Resources

- Streaming: https://platform.claude.com/docs/en/build-with-claude/streaming
- OpenAI Responses API: https://platform.openai.com/docs/api-reference/responses
