# 今日头条 MCP | Toutiao MCP

LobeHub 用户请使用 [LobeHub setup / 接入说明](LOBEHUB.md)，包含专属官网入口、认证和来源配置。

SocialDataX / 社媒数据助手 provides a hosted, read-only MCP service for public Toutiao data. This repository contains connection metadata and client examples.

## Connection

- Endpoint: `https://mcp.socialdatax.com/toutiao/mcp`
- Transport: `streamable-http`
- API Key: set `SOCIALDATAX_API_KEY` and send `Authorization: Bearer <SOCIALDATAX_API_KEY>`.
- Website and API Key access: <https://socialdatax.com/ai?from=github>
- Registry name: `com.socialdatax/toutiao`
- Local metadata: `0.1.2`, 14 tools including the shared points balance tool.
- Hosted discovery: `0.1.2`, 14 tools, verified on 2026-10-16.
- Official Registry: [`0.1.2`](https://registry.modelcontextprotocol.io/v0.1/servers/com.socialdatax%2Ftoutiao/versions/0.1.2), verified active/latest on 2026-10-16. Public repository and third-party directory status are verified separately.

## Capabilities

Search public posts and users, get search suggestions and hot searches, and read post details, comments, comment replies, creator profiles and creator posts.

The service does not provide account login, posting, editing, liking, following or writing comments.

## Tools

| Tool | Purpose |
| --- | --- |
| `toutiao_get_hot_search_list` | 读取今日头条热搜榜，返回头条当前热门关键词及上游热度信息。 |
| `toutiao_search_suggestions` | 获取今日头条搜索输入框的联想词；不返回用户或内容详情，不支持分页。 |
| `toutiao_search_users` | 按关键词查找今日头条用户，返回用户 ID、名称、简介、粉丝数和认证说明，支持分页；已有用户 ID 或主页链接时直接查询用户资料。 |
| `toutiao_get_user_info_by_user_id` | 读取头条用户资料和主页统计，缩略统计为近似值；已有数字用户 ID 时优先使用本工具，只有主页链接时使用 toutiao_get_user_info_by_profile_url。 |
| `toutiao_get_user_info_by_profile_url` | 通过用户主页链接或分享文案读取头条用户资料和主页统计，缩略统计为近似值；同时有数字用户 ID 时优先使用 toutiao_get_user_info_by_user_id。 |
| `toutiao_get_user_posts_by_user_id` | 读取头条用户发布的作品；已有数字用户 ID 时使用本工具，有主页链接时使用按主页链接查询的工具。 |
| `toutiao_get_user_posts_by_profile_url` | 通过头条用户主页链接读取其发布的作品；支持文章、视频和微头条及分页。 |
| `toutiao_get_post_comment_replies_by_comment_id` | 读取指定一级评论下的回复，按头条默认顺序分页；comment_id 取一级评论结果，续页保持该 ID，不要改用回复项自身的 ID。 |
| `toutiao_search_posts` | 按关键词或短语查找今日头条公开内容，支持分页。不用于读取指定链接的详情或查找用户；不返回导航、百科、用户及视频聚合面板。 |
| `toutiao_get_post_detail_by_post_id` | 读取头条文章、视频或微头条详情，包含正文、图片、作者和互动数据，视频含播放信息；输入内容数字 ID，可接续搜索结果。有链接时使用 toutiao_get_post_detail_by_url。视频说明不是语音转写。 |
| `toutiao_get_post_detail_by_url` | 通过头条内容链接或分享文案读取文章、视频或微头条详情；只有内容 ID 时使用 toutiao_get_post_detail_by_post_id。视频说明不是语音转写。 |
| `toutiao_get_post_comments_by_post_id` | 读取头条文章、视频或微头条的一级评论，按头条默认顺序返回，支持分页，不包含评论回复；输入内容数字 ID，支持接续搜索结果；有链接时使用 toutiao_get_post_comments_by_url。 |
| `toutiao_get_post_comments_by_url` | 通过头条内容链接或分享文案读取一级评论，按头条默认顺序返回，支持分页，不包含评论回复；只有内容 ID 时使用 toutiao_get_post_comments_by_post_id。 |
| `socialdatax_get_points_balance` | Query the current API Key account's SocialDataX points balance. |

For tools whose schema includes `page_token`, leave it empty on the first request and pass the returned `next_page_token` unchanged on the next request. Keep the same target, search terms and filters. Search suggestions do not return posts or user details. Use IDs and URLs returned by the service; do not derive them from display names.

## Client examples

- [Streamable HTTP](examples/streamable_http_config.json)
- [Codex](examples/codex_config.toml)
- [Cursor](examples/cursor_mcp.json)
- [Claude Desktop fallback](examples/claude_desktop_config.json)

The command/stdio fallback in [mcp.json](mcp.json) uses `mcp-remote`. Direct HTTP clients should use the hosted endpoint.

## Verification scope

2026-10-16 authenticated production checks returned 8 search items, a successful post detail, a valid empty comment list and 9 items on the next search page. Long pagination and comment replies were not checked.

## Metadata

[server-card.json](server-card.json) contains the tool descriptions and input schemas. The implementation is privately hosted. License: MIT for the public documentation and connection examples.
