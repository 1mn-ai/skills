---
name: 1mn-author-ranger
description: Design, validate, publish, and revise evidence-led Rangers in a connected 1mn.ai workspace through the 1mn Ranger Author MCP server. Use when a user asks Claude Code or Codex to create a new Ranger, customize an existing Ranger, turn a monitoring idea into an autonomous 1mn loop, or inspect the available Ranger sources and templates.
---

# Author a 1mn Ranger

Create a source-bounded judgment loop, not a generic scheduled prompt. Use the
live MCP contract as runtime authority; do not guess source names, tool names, or
frontmatter from memory.

## Connect when needed

If the `1mn-rangers` MCP tools are unavailable, read
[`references/setup.md`](references/setup.md). Ask the user to complete the
client's native OAuth flow in their browser, including workspace selection,
then resume after the client reconnects. Never request, echo, paste, or commit
an access or refresh token yourself.

## Authoring workflow

1. Call `ranger_sources` and `rangers_list`.
2. Express the requested behavior as this loop:

   `trigger → discover → decide → act → verify → gate → persist → hand off`

   The scheduler supplies the trigger. The selected source adapter supplies
   discovery. Ranger judgment decides what crosses the evidence bar. Acting is
   limited to a normalized run and constrained draft Ticket creation or update.
3. Name the safety posture before drafting:

   - **Verifiability:** define how the run proves source coverage and calls
     `submitRangerRun` exactly once, including honest `no_data` or `blocked`.
   - **Blast radius:** keep actions draft-only. Never instruct the Ranger to
     deploy, publish, merge, message customers, spend money, or close Tickets.
   - **Ambiguity:** define a concrete evidence and actionability threshold;
     below-bar findings go to scratchpad memory with a promotion trigger.
4. Choose exactly one live source. If the user describes a source that the MCP
   does not list, explain that a source adapter must exist before a Ranger can
   be authored; do not disguise web search or shell access as a new source.
5. Call `ranger_template` for that source. Preserve its runtime contract while
   specializing the judgment boundary, evidence bar, dedupe rules, and report
   shape for the user's goal.
6. For an edit, call `ranger_get` first. Keep the exact skill name and
   `ranger-source`; never fork an existing Ranger accidentally.
7. Draft one complete `SKILL.md`:

   - use a unique lowercase hyphenated `name`;
   - write a trigger-rich `description`;
   - copy only tools returned for the source and keep an explicit
     `allowed-tools` list;
   - declare `autonomous: true`, `routine-kind: ranger`, and the exact
     `ranger-source`;
   - include a human title in `metadata.title`;
   - require complete source-window coverage, history and scratchpad dedupe,
     exactly one normalized submission, a Ticket disposition for every
     report-grade finding, and an honest `deliverTicket` close-out;
   - keep Ticket briefs compact, evidence-linked, and framed as problems rather
     than speculative features.
8. Call `ranger_validate` with the complete file. Correct only what the live
   validator rejects, then validate again. Do not publish an unvalidated draft.
9. Call `ranger_publish` once. New Rangers are intentionally created disabled;
   tell the user to review and activate the Ranger in the 1mn Rangers UI. An
   existing enabled Ranger changes behavior on its next run, so summarize the
   material change before publishing it.
10. Report the exact Ranger name, source, schedule, version, activation state,
    and the loop's evidence bar. Do not claim it is running when
    `activationRequired` is true.

## Guardrails

- Treat MCP validation and capability results as authoritative over this file.
- Never call internal 1mn run tools directly; this skill uses only the
  authoring surface.
- Never create a Dogfooding Ranger through this workflow. Dogfooding Rangers
  require a Persona and browser configuration created in 1mn.
- Never use retired source keys even if an old workspace contains historical
  runs for them.
- Never add a second source to one Ranger. Cross-source synthesis belongs in a
  separate downstream loop.
