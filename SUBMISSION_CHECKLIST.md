# 今日头条 MCP 发布清单

- Product: SocialDataX / 社媒数据助手.
- Website: https://socialdatax.com.
- Hosted endpoint: https://mcp.socialdatax.com/toutiao/mcp.
- Registry name: `com.socialdatax/toutiao`; matches the existing hosted identity.
- Local metadata: `0.1.2` with 14 tools. Hosted discovery checked on 2026-10-16.
- Official Registry: [`0.1.2`](https://registry.modelcontextprotocol.io/v0.1/servers/com.socialdatax%2Ftoutiao/versions/0.1.2), verified active/latest on 2026-10-16.
- Public repository target: https://github.com/DevinChen2014/toutiao-mcp.

## Publication checks

1. Compare full inputSchema, tool names and annotations with hosted tools/list and runtime registration; reject top-level oneOf/anyOf/allOf.
2. Verify authenticated search, detail and list calls. Record actual results and limits; do not equate empty results with service failures.
3. Run mcp-publisher validate registry/toutiao/server.json in the private source repository.
4. Publish only public documentation, LICENSE, server-card, client configs, glama ownership and the brand logo; exclude keys, account data, raw samples and private implementation.
5. Confirm Registry active/latest and read GitHub files back by commit SHA. Record directory submission and public listing as separate states.

Use `Authorization: Bearer <SOCIALDATAX_API_KEY>` with hosted Streamable HTTP. Examples contain placeholders only. Do not change other platforms' Registry identities.
