# 项目：CodeArts 需求管理 MCP Server

> 最后更新：2026-10-27

## 项目总览

- 目标：完成华为 ICT 1.8，将 CodeArts Req 的创建项目和查询项目列表封装为 stdio MCP Server。
- 技术栈：Node.js 24、`@modelcontextprotocol/sdk`、原生 crypto/net/tls。
- 安装：`npm ci --registry=https://repo.huaweicloud.com/repository/npm/`。
- 测试：`npm test`。
- 启动：配置环境变量后执行 `npm start`。
- 入口：`server.mjs`。

## 当前状态

- 已完成：`create_project` 与 `list_projects` 工具定义。
- 已完成：参数 Schema、业务约束和中文结构化错误。
- 已完成：SDK-HMAC-SHA256 签名、可选 SOCKS5 请求路径。
- 已完成：59 项离线测试。
- 已完成：stdio 进程启动验证。
- 下一步：按需在码道配置个人 AK/SK 并调用真实 API。
- 卡点/风险：真实 API 调用需要用户自己的 AK/SK；测试未创建任何真实项目。

## 需求与约定

- 只使用免费资源。
- AK/SK 只通过环境变量注入。
- 不把 `.env`、真实 `mcp_settings.json` 或凭证提交到 Git。
- API 文档是参数 Schema 的事实来源。

## 待办 / 已知问题

- [x] 完成工具实现和离线测试。
- [ ] 创建并推送个人仓库。
- [ ] 用户需要时配置个人 AK/SK，并在码道验证真实调用。

## 版本历史

- 2026-10-27：完成 MCP Server、函数注释、配置样例、测试和交接文档。
