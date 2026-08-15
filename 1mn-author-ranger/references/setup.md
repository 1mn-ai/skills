# Connect the 1mn workspace MCP server

The MCP endpoint is:

```text
https://1mn.ai/api/mcp/rangers
```

It uses native MCP OAuth with PKCE. The browser flow asks the user to sign in,
approve Ranger and Ticket access, and choose exactly one 1mn workspace. The
client stores and refreshes its own credentials; never ask the user to paste a
token or add authentication headers manually.

## Claude Code

Add the Streamable HTTP server at user scope:

```bash
claude mcp add --transport http --scope user 1mn-rangers https://1mn.ai/api/mcp/rangers
```

Inside Claude Code, run `/mcp`, choose `1mn-rangers`, and authenticate. Complete
the 1mn browser prompt and return to Claude Code. Claude stores the credentials
securely and refreshes them automatically.

## Codex

Add this server to `~/.codex/config.toml`:

```text
[mcp_servers.1mn-rangers]
url = "https://1mn.ai/api/mcp/rangers"
auth = "oauth"
default_tools_approval_mode = "writes"
```

Then authenticate:

```bash
codex mcp login 1mn-rangers
```

Complete the browser prompt. Codex stores the OAuth credentials and refreshes
them automatically. The same connection is visible to Codex clients sharing
that host's MCP configuration.

After configuration, restart or reconnect the client and verify that
`ranger_sources` is visible before invoking the authoring skill. To change the
authorized workspace, clear/re-authenticate the server from the client's MCP
management UI and choose a different workspace in the 1mn consent screen.
