# Week 02: An MCP server with all the parts

Track: Under the hood

## Goal

Build a Model Context Protocol server for something fun (Home Assistant, Spotify, a Steam library, Plex, a 3D printer) that uses the parts most servers skip: resources, prompts, elicitation, sampling, and a remote HTTP transport with OAuth. Connect it to Claude Code, Codex, and claude.ai at the same time.

## Why it matters

Both Claude and Codex speak MCP. Most servers are a bag of tools. Knowing the whole spec means I can design servers that agents are actually good at using, and I can tell when a client is the problem instead of the server.

## Deliverable

A published server, running locally over stdio and remotely over HTTP, connected to three clients.

## Done when

- [ ] stdio and remote HTTP transports both work
- [ ] At least one resource, one prompt, and one elicitation flow
- [ ] OAuth on the remote transport
- [ ] Sampling used for at least one feature
- [ ] A notes file on how each client handled the same server differently

## Stretch

- Publish to an MCP registry
- Mark some tools for deferred loading and test tool search from the client side
- Write a second, deliberately bad version of one tool and measure how much worse the agent gets

## Resources

- MCP specification and docs: https://modelcontextprotocol.io
- Claude Code MCP docs: https://code.claude.com/docs/en/mcp
- Codex docs: https://developers.openai.com/codex
