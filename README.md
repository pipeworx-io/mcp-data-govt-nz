# @pipeworx/data-govt-nz

[data.govt.nz](https://catalogue.data.govt.nz/) MCP — NZ government CKAN open-data catalogue, keyless.

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1394+ live data sources.

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

Or connect to the full Pipeworx gateway for access to all 1394+ data sources:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English:

```
ask_pipeworx({ question: "your question about Data Govt Nz data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
