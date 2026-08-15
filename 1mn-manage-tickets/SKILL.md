---
name: 1mn-manage-tickets
description: Read, create, and refine Tickets in a connected 1mn.ai workspace through MCP. Use when a user asks Claude Code or Codex to inspect the Ticket backlog, review a Ticket and its timeline or artifacts, file new work for later, improve a Ticket title or brief, or turn local investigation into a reviewable 1mn Ticket without starting execution.
---

# Manage 1mn Tickets

Use Tickets as durable human handoffs. Keep creation and editing reviewable;
never imply that MCP authoring started an agent run.

## Connect when needed

If the `1mn-rangers` MCP tools are unavailable, read
[`references/setup.md`](references/setup.md). Ask the user to complete native
OAuth login and workspace selection, then resume after the client reconnects.
Never request, echo, paste, or commit an access or refresh token.

## Workflow

1. Call `tickets_list` before creating work when the request might duplicate an
   existing Ticket. Use `lifecycleStatus: "all"` only when closed history matters.
2. Call `ticket_get` before editing. Treat the current brief, activity timeline,
   and artifacts as the source of truth.
3. For new work, draft a compact problem-oriented Ticket:

   - title the observable outcome or problem, not an implementation guess;
   - put evidence, impact, constraints, assumptions, and the desired verification
     in `instructions`;
   - separate confirmed facts from inference;
   - search the backlog first and strengthen an existing open Ticket when it
     already owns the underlying problem.

4. Call `ticket_create` once. The result stays in the backlog with
   `executionStarted: false`; tell the user it must be reviewed and started in
   1mn.
5. Use `ticket_update` only for an open Ticket and only after reading it. Preserve
   useful existing evidence while clarifying the title or brief.
6. Report the exact `TKT-N` reference, lifecycle, what changed, and the remaining
   human action.

## Guardrails

- Never claim that creating or editing a Ticket started work, consumed quota,
  approved an artifact, merged code, or changed its lifecycle.
- Do not invent Ticket identifiers. Use the exact `ticketId` returned by
  `tickets_list`, `ticket_get`, or `ticket_create` for subsequent tool calls.
- Do not create one Ticket per observation. Group evidence by one underlying
  problem and preserve dedupe context in the brief.
- Do not overwrite a richer brief with a shorter summary. Make the smallest edit
  that resolves the user's request.
- Execution, completion, archive, artifact approval, deployment, and merge remain
  explicit 1mn UI gates.
