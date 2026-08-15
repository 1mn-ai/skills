# 1mn.ai skills

Open agent skills for connecting Claude Code and Codex to [1mn.ai](https://1mn.ai).

## Available skills

- [`1mn-author-ranger`](./1mn-author-ranger) — design, validate, and publish a
  source-bounded Ranger directly into a 1mn workspace through MCP.
- [`1mn-manage-tickets`](./1mn-manage-tickets) — inspect the backlog and safely
  create or refine reviewable Tickets without starting agent execution.

## Install

Install both skills and choose Claude Code, Codex, or another supported agent:

```bash
npx skills add 1mn-ai/skills
```

Or install one skill directly:

```bash
npx skills add 1mn-ai/skills --skill 1mn-author-ranger
npx skills add 1mn-ai/skills --skill 1mn-manage-tickets
```

## Connect the MCP

The MCP endpoint is `https://1mn.ai/api/mcp/rangers`.

### Claude Code

```bash
claude mcp add --transport http --scope user 1mn-rangers https://1mn.ai/api/mcp/rangers
```

Run `/mcp` inside Claude Code, select `1mn-rangers`, and authenticate.

### Codex

```bash
codex mcp add 1mn-rangers --url https://1mn.ai/api/mcp/rangers
codex mcp login 1mn-rangers
```

Complete the browser flow to sign in, approve Ranger and Ticket access, and
choose a 1mn workspace. The client stores and refreshes the OAuth credentials,
so no API token or recurring manual login is required.

Then invoke `$1mn-author-ranger` or `$1mn-manage-tickets`.
