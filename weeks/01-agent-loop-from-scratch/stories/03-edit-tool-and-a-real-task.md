# Story 1.3: Edit tool and a real task

Time: two hours. Prerequisite: story 1.2.

## Goal

Add read and edit tools, point the agent at a real repo of yours, and have it make one small real change (fix a bug, add a test, tidy a function) with the tests passing.

## Afterward you can explain

- How tool descriptions and schemas shape what the model does
- Why a search-and-replace edit beats "write the whole file"
- What a read tool needs to give the model (line numbers, limits)

## Guide for the agent

1. Before any code, have the learner list the minimum tools a coding agent needs. Compare with Claude Code's set: Read, Edit, Write, Bash, Glob, Grep. Which are conveniences over bash, and which exist for safety or token reasons?
2. Have them implement `read_file` (path, optional offset and limit, returns numbered lines) and `edit_file` (path, old_string, new_string, fails unless old_string is unique). They write the descriptions. Then ask: could you use this tool from the description alone?
3. Pick a real, small task in the target repo (widgethub, or another with tests). Run the agent with a system prompt naming the repo root and the test command.
   Checkpoint: before running, have them predict how many tool calls it will take.
4. Review the diff together as if a colleague opened it as a PR. Run the tests.
5. Experiment: make the edit tool's description vague ("edits a file") and rerun the same task. Compare behavior and token use.
   Checkpoint: what changed, and why?
6. Add `strict: true` to the tool definitions (with `additionalProperties: false` and `required`) so inputs are guaranteed to match the schema.

Point out when it comes up:

- A tool description is prompt. A schema is a contract. They do different jobs.
- Claude Code's Edit tool requires the old text to be unique for the same reason theirs should.

## Done when

- [ ] Read and edit tools with descriptions the learner would trust
- [ ] A real change landed in a real repo, tests green, reviewed by the learner
- [ ] The vague-description experiment logged with numbers
- [ ] Tools use strict mode

## Log prompt

What did the agent do that you wouldn't have done? Was it better or worse?

## Resources

- Strict tool use: https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview
- Anthropic, "Writing tools for agents": https://www.anthropic.com/engineering/writing-tools-for-agents
