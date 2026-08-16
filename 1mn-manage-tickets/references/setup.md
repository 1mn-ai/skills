# Connect the 1mn workspace MCP server

The MCP endpoint is:

```text
https://1mn.ai/api/mcp
```

It uses native MCP OAuth with PKCE. The browser flow asks the user to sign in,
approve Ranger and Ticket access, and choose exactly one 1mn workspace. The
client stores and refreshes its credentials; never add authentication headers
or paste tokens manually.

## Claude Code

```bash
claude mcp add --transport http --scope user 1mn-rangers https://1mn.ai/api/mcp
```

Run `/mcp`, choose `1mn-rangers`, and authenticate in the browser.

## Codex

Add this server to `~/.codex/config.toml`:

```text
[mcp_servers.1mn-rangers]
url = "https://1mn.ai/api/mcp"
auth = "oauth"
default_tools_approval_mode = "writes"
```

Then run:

```bash
codex mcp login 1mn-rangers
```

After authentication, reconnect the client and verify that `tickets_list` is
visible. To change workspace or grant newly-added Ticket scopes, clear and
reauthenticate the MCP connection.
