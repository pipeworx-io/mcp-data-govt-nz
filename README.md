# @pipeworx/data-govt-nz

[data.govt.nz](https://catalogue.data.govt.nz/) MCP — NZ government CKAN open-data catalogue, keyless.

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1663+ live data sources.

## Tools

- `package_list(limit?, offset?)` — list dataset names (paged)
- `package_search(q?, fq?, sort?, rows?, start?, facet_field?)` — full-text + faceted search
- `package_show(id)` — single dataset (id or name)
- `organization_list(all_fields?, limit?, offset?)` — publishing orgs
- `organization_show(id, include_datasets?)` — single org
- `group_list(all_fields?, limit?, offset?)` — groups/categories
- `group_show(id, include_datasets?)` — single group
- `tag_list(query?, all_fields?, vocabulary_id?)` — tag list
- `tag_show(id, include_datasets?)` — single tag
- `recently_changed_packages(limit?, offset?)` — recent updates
- `resource_show(id)` — single resource

## Data source

`https://catalogue.data.govt.nz/api/3/action`

## Quick Start

Add to your MCP client (Claude Desktop, Cursor, Windsurf, etc.):

```json
{
  "mcpServers": {
    "data-govt-nz": {
      "url": "https://gateway.pipeworx.io/data-govt-nz/mcp"
    }
  }
}
```

### What this endpoint actually serves

`tools/list` at `https://gateway.pipeworx.io/data-govt-nz/mcp` returns the tools in the table
above **plus the shared Pipeworx meta-tools** — `ask_pipeworx`,
`discover_tools`, `search_within`, `remember`/`recall` and the rest of the
gateway-wide set. So the tool count you see is larger than this table: a
single-pack endpoint currently lists roughly 30 shared tools alongside the
pack's own. The connection's `initialize` response states its exact scope, and
is the authoritative answer for a given day.

This is deliberate, not multiplexing by accident. The meta-tools are what let a
scoped connection answer a question this pack does not cover — via
`ask_pipeworx`, which routes across the whole catalog — without you adding a
second MCP server. There is currently no way to mount a pack endpoint without
them; if the extra schemas cost you more context than the routing is worth,
connect to the full gateway once rather than to several pack endpoints.

Or connect to the full Pipeworx gateway to get every pack's tools listed
directly, instead of just this one's:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

Both URLs reach the same gateway and the same 1663+ data sources. The
only difference is which pack's tools are listed **directly**; `ask_pipeworx`
reaches all of them from either one.

## No MCP client? Call it over HTTP

```bash
curl -X POST https://gateway.pipeworx.io/v1/tools/data_govt_nz_package_list \
  -H 'Content-Type: application/json' \
  -d '{"limit":10,"offset":0}'
```

No account needed for the first calls. Inspect any tool: `GET https://gateway.pipeworx.io/v1/tools/data_govt_nz_package_list`. Find one: `POST https://gateway.pipeworx.io/v1/tools/search_packs` with `{"query":"..."}`.

## Standalone (no gateway account)

This package also runs as a local stdio MCP server — no Pipeworx account, no
gateway round-trip:

```json
{
  "mcpServers": {
    "data-govt-nz": {
      "command": "npx",
      "args": ["-y", "@pipeworx/mcp-data-govt-nz"]
    }
  }
}
```

Or run it directly to confirm it starts:

```bash
npx -y @pipeworx/mcp-data-govt-nz
```

It speaks MCP over stdin/stdout and answers `initialize`/`tools/list`/`tools/call`
for **only** this pack's tools — none of the shared meta-tools the gateway
connection above adds. Same source, same tools, no ask_pipeworx routing.

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English —
this works on the pack endpoint above as well as on the full gateway:

```
ask_pipeworx({ question: "your question about Data Govt Nz data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
