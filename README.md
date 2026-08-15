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

Then invoke `$1mn-author-ranger` or `$1mn-manage-tickets`. The workspace MCP
server uses native OAuth:
Claude Code or Codex opens 1mn in the browser for login, consent, and workspace
selection, then refreshes the connection automatically.
