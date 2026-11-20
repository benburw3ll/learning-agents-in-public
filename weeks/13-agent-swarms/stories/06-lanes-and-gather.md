# Story 13.6: Lanes, gather and conflicts

Time: about an hour. Prerequisite: story 13.5 (its saved briefs).

## Goal

Run a build swarm end to end: lanes, builders, gather, one run of the full suite, one review, one simulated PR. Then break a gather on purpose and resolve it calmly.

## Afterward you can explain

- What a worktree is and why each builder gets its own
- Why gather cherry-picks instead of merging
- What to do when gather stops on a conflict
- Why the lead runs the full suite after gathering even though every builder's tests passed

## Key ideas

A **worktree** is a second folder holding the same repo on a different branch. All worktrees share one `.git`, so a commit in one is instantly a branch the others can see, but each folder has its own files. A **lane** is one builder's worktree:

```
swarm branch:   fix/dojo-sweep                     (the lead's checkout)
lane branches:  fix/dojo-sweep--money   →  <repo>/.claude/worktrees/fix-dojo-sweep--money
                fix/dojo-sweep--cli     →  <repo>/.claude/worktrees/fix-dojo-sweep--cli
```

The kit's four scripts, all run from the swarm's checkout:

- `lanes.sh <name>...` cuts one lane per name from the current HEAD (refusing on `main` or with uncommitted work), installs dependencies, and prints `<name> <path> <port>`. The port is that lane's own dev-server port, so two lanes never fight over a server.
- `status.sh` prints one line per lane: commits ahead, uncommitted files, path.
- `gather.sh` brings each lane back by **cherry-pick**, so history stays a straight line and each builder's commit messages (and `Refs #n` lines) survive as they are. Then it removes the lane's worktree and branch. It refuses a lane with uncommitted changes and stops on a conflict, naming the lane.
- `busy.sh` lists files other worktrees and open PRs already hold.

**When gather conflicts:** resolve the file (usually keeping both changes), `git add` it, `git cherry-pick --continue` (which also picks the rest of that lane's commits), then run `gather.sh` again. It has to recognise the commits already gathered. A cherry-picked copy never moves the merge-base, so a naive script re-picks the lane and conflicts again, forever. Mine did, until building this drill found it. Matching on author, author date and subject, which a cherry-pick keeps, fixed it.

**Windows:** never `cd` into a lane from the lead's shell. Windows can't delete a folder a shell is sitting in, so gather's clean-up fails with EPERM. Read lanes with `git -C <lane> ...`.

**After gathering:** run the full suite once (lanes can pass alone and break together). Review once, on `origin/main...HEAD`. The lanes are gone by then, so review fixes are the lead's commits on the same branch. A builder that missed something before gathering is better continued with SendMessage: it still has its lane and its context.

## Guide for the agent

1. Rebuild with the board: `node ~/.claude/skills/swarm-school/labs/seed-dojo.mjs ~/swarm-dojo --reset --board`. Have the learner make the swarm branch: `git -C ~/swarm-dojo switch -c fix/dojo-sweep`. (In a real repo this is its own worktree off `origin/main`; the dojo has no other sessions.)
2. Have the learner cut the lanes: `cd ~/swarm-dojo && bash ~/.claude/skills/swarm/scripts/lanes.sh money cli`.
   Checkpoint: what did it just create, and where? Have them confirm with `git -C ~/swarm-dojo worktree list`.
3. Launch both `swarm-builder` members in one message with `model: "sonnet"`, using the briefs from `~/swarm-dojo-briefs.md` with the lane paths `lanes.sh` printed. If that file is missing, the learner rewrites them from the split in `dojo-answer-key.md`.
4. The lead's share while they run: the learner settles #7 the way they decided in 13.5 (in files no lane owns) and adds the changelog lines under "## Unreleased", committed on `fix/dojo-sweep`. Run `bash ~/.claude/skills/swarm/scripts/status.sh` once from `~/swarm-dojo` to show what it reports. No polling.
5. When both report, the learner reads each report's "Outside my files" and checks one lane themselves: `git -C <lane> log --oneline fix/dojo-sweep..` and `git -C <lane> diff fix/dojo-sweep --stat`.
   Checkpoint: does the report match the diff? A report is a claim.
6. Gather: `cd ~/swarm-dojo && bash ~/.claude/skills/swarm/scripts/gather.sh`, then `npm run check` once.
7. Review: one `swarm-reviewer` on `~/swarm-dojo`, `model: "sonnet"`, range `origin/main...HEAD`, angle "correctness and the AGENTS.md rules", under 300 words. Compare its findings with the reference fixes in the answer key. The learner applies what's real as commits on `fix/dojo-sweep`, and runs the suite again only if code changed.
8. The "PR" and the "merge": `git -C ~/swarm-dojo push -u origin fix/dojo-sweep`, then `git -C ~/swarm-dojo switch main`, `git -C ~/swarm-dojo merge --ff-only fix/dojo-sweep` and `git -C ~/swarm-dojo push origin main`. `git -C ~/swarm-dojo worktree list` should show one checkout.
   Checkpoint: did the split hold? Did a builder go outside its files? Did the suite or the reviewer catch something the builders' own tests missed?
9. The conflict drill, no agents. Two lanes both add a line in the same place in `CHANGELOG.md`, which is what happens when nobody owns the hot file:
   ```
   node ~/.claude/skills/swarm-school/labs/seed-dojo.mjs ~/swarm-dojo --reset
   cd ~/swarm-dojo && git switch -c chore/conflict-drill && bash ~/.claude/skills/swarm/scripts/lanes.sh a b
   node ~/.claude/skills/swarm-school/labs/changelog-line.mjs ~/swarm-dojo/.claude/worktrees/chore-conflict-drill--a "Lane a fixed the split."
   git -C ~/swarm-dojo/.claude/worktrees/chore-conflict-drill--a commit -qam "docs: changelog line from lane a"
   node ~/.claude/skills/swarm-school/labs/changelog-line.mjs ~/swarm-dojo/.claude/worktrees/chore-conflict-drill--b "Lane b fixed the store."
   git -C ~/swarm-dojo/.claude/worktrees/chore-conflict-drill--b commit -qam "docs: changelog line from lane b"
   cd ~/swarm-dojo && bash ~/.claude/skills/swarm/scripts/gather.sh
   ```
   Expected: lane a gathers, lane b stops with `UU CHANGELOG.md`.
   Checkpoint: the learner looks at the conflict markers and says how to resolve them before touching anything.
10. The learner resolves it (keeps both lines), then `git add CHANGELOG.md`, `GIT_EDITOR=true git cherry-pick --continue`, and `bash ~/.claude/skills/swarm/scripts/gather.sh` again. Expected: `lane b: its 1 commit(s) are already gathered`, and the lanes are removed.
    Checkpoint: which line of a plan would have prevented this conflict? (The lead owns `CHANGELOG.md`.)

Point out when it comes up:

- Builders `cd` into their own lane; that's their shell, not yours.
- Gather refusing a lane with "UNCOMMITTED changes" means a builder forgot to commit. Look with `git -C <lane> status`, then commit there or continue the builder.

## Done when

- [ ] Two builders worked in two lanes and gathered without a conflict
- [ ] The full suite passed once after gathering
- [ ] One review done, real findings fixed on the same branch
- [ ] The conflict drill resolved, with the second gather finishing cleanly

## Log prompt

What did the full suite or the reviewer catch that the builders' own tests didn't? If nothing, why not?

## Resources

- Git worktrees: https://git-scm.com/docs/git-worktree
- Git cherry-pick: https://git-scm.com/docs/git-cherry-pick
