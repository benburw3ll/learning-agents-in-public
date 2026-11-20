# Story 13.7: Techniques and anti-patterns

Time: about 30 minutes. Prerequisite: story 13.6. A drill: no agents.

## Goal

Reach for the right technique when a job doesn't fit a preset, and spot a broken swarm plan before it spends anything.

## Afterward you can explain

- Seam first, waves, and scout-then-build, and when each one applies
- Why you continue a member instead of starting a new one
- The common failure symptoms and the planning mistake behind each

## Key ideas

Twelve techniques:

1. **The lead's share.** While members run, the lead takes the piece that needs the most context: the product call, the hot files, the docs, the seam.
2. **Seam first.** Shared interfaces land on the swarm's branch before the lanes are cut.
3. **Waves.** If piece B needs piece A's result, they aren't parallel. Run A, gather, then cut B's lanes from the new HEAD.
4. **Scout, then build.** Two cheap Sonnet scouts map where a change touches; the lead turns the map into the file split. Builders then start knowing where to work, instead of each rediscovering the codebase at Opus prices.
5. **Continue, don't respawn.** A builder that missed a "Done when" box gets a SendMessage before gathering: it still has its lane and its context. A new member starts cold.
6. **Shape the output for the gather.** Ask for what you'll consume (an edit list, issue drafts in the repo's shape, a table), so the gather is mechanical.
7. **Rank by cost.** Without a ranking, a typo and a money bug arrive with equal weight.
8. **Red-team reviewer.** One reviewer's whole job is finding inputs that break the change.
9. **Redundancy, rarely.** Two scouts on one high-stakes question, with different models or framings. Agreement is confidence; disagreement is where to look. It doubles the cost.
10. **Mix models by the cost of a miss.** Sonnet to read, Opus to write and judge, Haiku to clean up, the top model only where a miss is costly.
11. **One stop line, said once.** A usage limit goes in every brief once. No updates mid-run.
12. **A report is a claim.** Run the suite and read the diff before calling anything done.

Sometimes the members should be sessions rather than subagents: long-lived peers with real judgement that you'll want to steer. The rules are the same (clear roles, files that don't overlap, one lead that keeps the design); it costs more and is slower to coordinate.

| Symptom | Cause | Fix |
| --- | --- | --- |
| 10 agents, 3 real pieces | over-swarming | as many members as independent pieces |
| gather conflicts every time | split by issue count; shared hot files | split by files; one owner per hot file; seam first |
| two scouts return the same findings | overlapping angles | orthogonal angles; "the others cover" |
| the lead gets slow and forgetful | no word limits | word limits; ranked findings |
| members finish one after another | launched in separate messages | one message for all of them |
| turns spent checking on agents | polling | they run in the background; you're notified |
| a PR per builder or per pass | no gather | one branch, one PR; passes are more commits in the same lane |
| a member stops to ask a question | no never-ask line | put it in the brief |
| a builder edited the main checkout | no lane, or no lane path in the brief | `lanes.sh`; the path in the brief |
| "Done!" but the suite fails | the report was trusted | run the suite once after gathering; read the diff |
| a re-review after the merge; a second PR for the same ask | not knowing when to stop | review once, before the PR; new findings go on the board |
| expensive agents doing cleanup | no housekeeper | one Haiku housekeeper, or the lead |
| a brief that says "as we discussed" | forgetting the cold start | put the context in the brief |
| a wave-2 builder works on stale code | dependent pieces launched together | gather wave 1 first |

## Guide for the agent

1. Give the learner all six plans in one message. For each, they name the anti-pattern(s) and the fix.
   1. "Build swarm: 6 builders for the 6 issues in the milestone, one issue each." Two of the issues touch the same folder.
   2. "QA swarm: 4 scouts, angles: bugs, code quality, correctness, problems."
   3. "Launched scout 1. Now launching scout 2. Now scout 3."
   4. "Builders: when you're done, open a PR and send me the link."
   5. "Reviewer brief: review the stuff we changed today and let me know what you think."
   6. "Builder A adds the `exportData` API; builder B builds the export screen that calls it. Launch both now."
   Checkpoint: grade. Expected: split by issue count, two lanes in one folder → group by files, probably 3–4 lanes; overlapping angles → orthogonal angles plus "the others cover"; separate messages → one message; builders never push or open PRs → the lead gathers into one PR; cold-start context, no range, no angle, invites a question, no word limit → name the checkout, `origin/main...HEAD`, one angle, findings with fixes, under 500 words; B depends on A → seam first (the lead lands the API's signature) or two waves.
2. Have the learner pick the one technique they'd most likely have missed on their own and say where it would have helped in the 13.6 lab.
   Checkpoint: is that a real fit, or would the lab have gone the same way without it?
3. Checkpoint: builder `money` reports it skipped the "1,200.00" test, and you haven't gathered yet. New member or continue the old one? (Continue it with SendMessage; it keeps its lane and context.)

Point out when it comes up:

- Almost every row in the table is a planning failure, not an execution one. That's why 13.5 grades the plan before 13.6 runs it.

## Done when

- [ ] The six plans diagnosed, with at least five right
- [ ] You can explain seam first, waves and scout-then-build with an example of your own

## Log prompt

Which anti-pattern have you already done for real, before this week?
