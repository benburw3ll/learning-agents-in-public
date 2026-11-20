# Story 13.1: What a swarm is

Time: about 30 minutes. Prerequisite: the swarm kit installed (see the stories README).

## Goal

Replace "a team of agents working together" with the real shape: one lead, isolated members, one brief down and one report back each. Prove to yourself that a member knows only what its brief says.

## Afterward you can explain

- Why a swarm is a hub, not a group chat
- The three things a swarm buys (time, independent eyes, a clean lead context) and what it costs
- Why the brief is the member's whole world

## Key ideas

```
                 ┌──────────── lead (your session) ────────────┐
   brief ──▶ scout A        brief ──▶ scout B        brief ──▶ builder C
   report ◀──               report ◀──               commits + report ◀──
```

- A member sees its **role file** (`~/.claude/agents/swarm-*.md`, the rules every member of that role follows), the **brief**, and the **repo and tools**. It never sees your conversation, your memory files, or the other members.
- A member returns **one final message**. That report is all the lead gets back.
- **What it buys:** time (four ten-minute audits finish in about ten minutes); independent eyes (each angle gets a fresh context with nothing else on its mind); context protection (a scout reads 200k tokens of logs and hands back 500 words, so the lead stays sharp).
- **What it costs:** tokens (every member starts cold, so four members cost about four cold starts, never less than one agent reading the same things); merge work for members who write; the lead's attention for splitting, briefing and gathering.
- **Myths:** members collaborate (they can't see each other); more agents is better (not past the number of independent pieces); members know the context (they know the brief); a swarm is several sessions (members are subagents inside one session; separate sessions are a different, heavier tool).

## Guide for the agent

1. Ask the learner to describe a swarm in one sentence and to say who talks to whom.
   Checkpoint: compare their answer with the hub picture. Name what's missing, usually "members can't see each other or the conversation".
2. Build the dojo: `node ~/.claude/skills/swarm-school/labs/seed-dojo.mjs ~/swarm-dojo --reset`. Have the learner run `npm run check` in `~/swarm-dojo` (8 tests pass) and read its README.md.
3. Show the lazy brief, verbatim: `Check the split thing we talked about and tell me if it's OK. The repo is ~/swarm-dojo.` Have the learner write a full brief for the same job: find out whether money is ever lost when a bill is split, checked against the README's promise that shares always add up to the total. It needs a goal, the exact files, the promise to check against, the output shape, a word limit (250) and a never-ask line.
   Checkpoint: before anything launches, the learner predicts what the lazy scout will come back with.
4. Launch both `swarm-scout` members in one message, on Sonnet (the role default), one per brief.
5. When both report, put them side by side.
   Checkpoint: which lines of the full brief made the difference? (Expected: the lazy scout guesses at "the split thing" or reviews something generic; the full one pins `splitEvenly(1000, 3)` returning 333 three times, with a fix.)
6. Two quick questions, one at a time:
   Checkpoint: a member's report says "as you mentioned earlier, the store is fine". What happened? (It can't know what was mentioned. It filled a gap with a guess: treat the claim as unverified and put the context in the next brief.)
   Checkpoint: one bug, one file. Swarm? (No. Inline; at most one subagent if finding the bug needs a big search.)

Point out when it comes up:

- Both scouts ran at the same time, and the session was notified as each finished. Nobody polled.
- The lead's context received two short reports, not the files the scouts read. That's the context protection.

## Done when

- [ ] Two scouts ran in one message, one with each brief
- [ ] You can say which lines the lazy brief was missing, and what each one would have prevented
- [ ] You can name what a swarm buys and what it costs without looking

## Log prompt

What did you predict the lazy scout would do, and what did it actually do?

## Resources

- Claude Code subagents: https://code.claude.com/docs/en/sub-agents
