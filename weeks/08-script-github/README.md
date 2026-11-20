# Week 08: Script GitHub

Track: GitHub deep end

## Goal

Use the GitHub CLI and GraphQL API for the things the web UI makes tedious: Projects, rulesets, merge queues, reusable workflows, release automation, and Dependabot auto-merge. Then build a tiny GitHub App with webhooks that does something real, like a weekly digest of my repos written by an agent.

## Why it matters

GitHub is the surface every agent workflow lands on. Being fluent in its API means agents can drive it too.

## Deliverable

A repo of mine with rulesets, a merge queue, and release automation, plus a running GitHub App.

## Done when

- [ ] Rulesets and a merge queue on a repo of mine
- [ ] Release automation that cuts a release from conventional commits
- [ ] A GitHub App that receives webhooks and posts something
- [ ] A GraphQL query I use weekly, saved as a gh alias
- [ ] Dependabot auto-merge for patch updates, gated on CI

## Stretch

- Projects v2 automation via GraphQL
- A reusable workflow shared across two repos

## Resources

- GitHub CLI: https://cli.github.com/manual
- GitHub GraphQL API: https://docs.github.com/en/graphql
- GitHub Apps: https://docs.github.com/en/apps
- Rulesets: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets
