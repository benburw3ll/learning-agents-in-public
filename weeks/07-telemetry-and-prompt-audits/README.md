# Week 07: Telemetry and prompt audits

Track: Measure

## Goal

Export Claude Code OpenTelemetry metrics into local Prometheus and Grafana. Dashboard cost per task, tokens per session, tool calls, and which skills and hooks fire. Then run a prompt audit over every instruction file I own and remove what's stale.

## Why it matters

I can't improve what I don't see, and instructions written for older models quietly degrade output until someone looks.

## Deliverable

A dashboard with a week of real data and at least one decision made from it, plus a cleaned-up config.

## Done when

- [ ] Dashboard with cost per session and per model
- [ ] A panel for which skills and hooks fire
- [ ] Prompt audit done across CLAUDE.md, skills, and subagents; stale instructions removed
- [ ] One week of data collected and one concrete decision made from it
- [ ] The dashboard runs from a single compose file

## Stretch

- An alert when a session burns past a budget
- Add Codex usage to the same dashboard

## Resources

- Claude Code monitoring: https://code.claude.com/docs/en/monitoring-usage
- OpenTelemetry: https://opentelemetry.io
- Grafana: https://grafana.com/docs
