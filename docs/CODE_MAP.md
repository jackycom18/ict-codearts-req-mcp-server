# 代码地图

> 最后更新：2026-10-27

## 总体结构

```text
codearts-req-mcp-server/
├─ server.mjs                 # MCP Server 和 CodeArts Req API 封装
├─ server.test.mjs            # 59 项离线测试
├─ package.json
├─ package-lock.json
├─ mcp_settings.example.json  # 安全配置样例
├─ .env.example
└─ docs/
```

## 逐文件核心内容

### `server.mjs`

- 用途：启动 stdio MCP Server，暴露创建项目和查询项目工具。
- 关键工具：`create_project`、`list_projects`。
- 鉴权：`buildSignature` 生成 SDK-HMAC-SHA256 请求头。
- 请求：`callApi` 统一处理查询参数、请求体、HTTP 与响应解析。
- 错误：`INVALID_ARGUMENTS`、`MISSING_CONFIG`、`NETWORK_ERROR` 和 API 原始错误。

### `server.test.mjs`

- 用途：注入 fetch 和配置，验证所有参数边界与成功/失败路径。
- 注意：不请求真实华为云接口，不需要 AK/SK。

### `mcp_settings.example.json`

- 用途：展示 stdio MCP 配置结构。
- 注意：AK/SK 必须由用户替换，样例不包含真实凭证。
