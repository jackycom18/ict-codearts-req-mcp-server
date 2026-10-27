# CodeArts 需求管理 MCP Server 设计

> 目标判据：华为 ICT 1.8 实验手册与“只使用免费资源”的约束。

## 目标

使用 Node.js 和 `@modelcontextprotocol/sdk` 实现 stdio MCP Server，将华为云 CodeArts Req 的创建项目、查询项目列表封装为智能体可调用工具。

## 工具契约

### `create_project`

- 调用：`POST /v4/project`
- 必填：`project_name`、`project_type`
- 可选：`description`、`enterprise_id`、`source`、`template_id`
- 当 `project_type=ipd` 时必须提供 `template_id`
- 返回项目 ID、数字 ID、名称、类型和用户数字 ID

### `list_projects`

- 调用：`GET /v4/projects`
- 可选：`offset`、`limit`、`search`、`project_type`、`sort`、`archive`、`query_type`
- `offset` 必须是 `limit` 的整数倍
- 返回项目数组和总数

## 鉴权与错误

- 终端节点从 `CODEARTS_REQ_ENDPOINT` 读取。
- AK/SK 从 `CODEARTS_REQ_AK`、`CODEARTS_REQ_SK` 读取，不进入代码和 Git。
- 使用 SDK-HMAC-SHA256 签名，携带 `Authorization` 与 `X-Sdk-Date`。
- 参数错误返回 `INVALID_ARGUMENTS`。
- 缺少配置返回 `MISSING_CONFIG`。
- 网络异常返回 `NETWORK_ERROR`。
- API 业务错误透传原始错误码、消息和 HTTP 状态。
- 所有错误都使用 `isError: true` 的结构化中文结果。

## 工程结构

- `server.mjs`：MCP 服务、工具定义、参数校验、AK/SK 签名和 API 请求。
- `server.test.mjs`：注入 fetch 的离线测试，不调用真实云资源。
- `package.json`：启动和测试入口。
- `README.md`：安装、环境变量、启动和码道配置。
- `docs/PROJECT_MEMO.md`、`docs/CODE_MAP.md`：交接文档。

## 验证

- `npm test` 的 59 项测试全部通过。
- `npm start` 能启动 stdio MCP 进程。
- 在未设置 AK/SK 时测试仍不访问真实 API。
- README 的配置示例不包含真实凭证。
