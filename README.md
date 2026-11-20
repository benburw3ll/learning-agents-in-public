# Learning Agents in Public

A public, week-by-week log of getting seriously good at agentic coding: Claude Code, Codex, MCP, and the GitHub machinery around them.

Platform engineer by day. At home I pay for the top tiers of both Claude and Codex, and this repo is how I make sure that money turns into skill instead of vibes. Every week has one concrete deliverable, a "done when" checklist, and a short write-up of what surprised me.

Started: November 2026.

## Why this exists

- Learn the tools from underneath, not just from the prompt box.
- Measure what works instead of guessing.
- Build things other people can install.
- Leave a trail a stranger can follow.

## The curriculum

Twelve weeks in four tracks. Each week links to its brief. Status: ⬜ not started · 🟨 in progress · ✅ done

| Wk | Track | Topic | Deliverable | Status |
|---:|-------|-------|-------------|:------:|
| 01 | Under the hood | [Agent loop from scratch](weeks/01-agent-loop-from-scratch/README.md) | A working coding agent in a few hundred lines, then the same on the Agent SDK | ⬜ |
| 02 | Under the hood | [An MCP server with all the parts](weeks/02-mcp-server-all-the-parts/README.md) | A server using resources, prompts, elicitation, sampling, remote transport with OAuth | ⬜ |
| 03 | Under the hood | [Mod the tools](weeks/03-mod-the-tools/README.md) | A Claude Code plugin and a Codex plugin that set up a fresh machine in one command | ⬜ |
| 04 | Under the hood | [Red-team your own agents](weeks/04-red-team-your-own-agents/README.md) | Documented injection attempts plus a sandboxed setup that survives them | ⬜ |
| 05 | Measure | [Hill-climb your CLAUDE.md](weeks/05-hill-climb-your-claude-md/README.md) | An eval set with a held-out split and three data-driven rounds of changes | ⬜ |
| 06 | Measure | [Cross-model duels](weeks/06-cross-model-duels/README.md) | Ten tasks run through both tools, cross-reviewed, with a scoreboard | ⬜ |
| 07 | Measure | [Telemetry and prompt audits](weeks/07-telemetry-and-prompt-audits/README.md) | A Grafana dashboard of cost per task and skill triggers, plus a cleaned-up config | ⬜ |
| 08 | GitHub deep end | [Script GitHub](weeks/08-script-github/README.md) | Rulesets, merge queue, release automation, and a small GitHub App that posts something real | ⬜ |
| 09 | GitHub deep end | [Agents in CI](weeks/09-agents-in-ci/README.md) | Claude Code and Codex reviewing PRs on my repos, tuned until I'd keep them | ⬜ |
| 10 | GitHub deep end | [Jujutsu, stacked PRs, open source](weeks/10-jujutsu-stacked-prs-open-source/README.md) | Two weeks on jj, a landed 3-PR stack, one upstream PR merged | ⬜ |
| 11 | Build | [Build your own X](weeks/11-build-your-own-x/README.md) | An emulator, a Redis clone, or a CodeCrafters track, driven with agents | ⬜ |
| 12 | Build | [Capstone: a personal assistant on the Agent SDK](weeks/12-capstone-personal-assistant/README.md) | One always-on bot using my own MCP servers, driven from my phone | ⬜ |

## How it's organized

- `weeks/NN-topic/README.md` is the brief: goal, why it matters, deliverable, done-when checklist, stretch goals, resources.
- `weeks/NN-topic/stories/` holds the guided stories for that week, in order. A Claude Code session in this repo tutors each one; the rules are in `CLAUDE.md`.
- `weeks/NN-topic/LOG.md` is the write-up, filled in as the week happens.
- Bigger builds get their own repository and are linked from the week that produced them.

## Ground rules

- Real repos, not demos. Every week's work lands somewhere I actually use.
- One feature a week, used for real, beats ten features skimmed.
- The log gets written the same day the work happens, while the surprises are fresh.
- Weeks can slip. The order can change. The checklist does not get quietly shortened.

## Tools in rotation

Claude Code (desktop app, CLI, cloud sessions, Agent SDK) · Codex (CLI, cloud, IDE) · Model Context Protocol · GitHub CLI, Actions, and Apps · Jujutsu · OpenTelemetry with Prometheus and Grafana

## Latest

No weeks finished yet. The first log entry will show up here.
