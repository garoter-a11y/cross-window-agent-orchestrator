# WinApp MCP 安装与接入 Hermes

> 来源：2026-06-16 会话，从零安装到54工具就绪

## 环境要求

- Node.js ≥ 22（已确认 v24.16.0 通过）
- .NET SDK **不需要**（npm 包自包含 .NET 运行时 + FlaUI，152MB）
- Windows 10/11

## 安装步骤

### 1. 全局安装

```bash
npm install -g winapp-mcp
```

验证：`which winapp-mcp` → shell wrapper → 调用 `server/WinAppMCP.exe`

### 2. 接入 Hermes MCP

```bash
hermes mcp add winapp --command "C:/Users/Administrator/AppData/Roaming/npm/node_modules/winapp-mcp/server/WinAppMCP.exe"
```

注意：`hermes mcp add` 有交互式确认（"Enable all 54 tools? [Y/n/select]:"），用 `echo "y" |` 管道自动应答。

### 3. 验证

```bash
hermes mcp list
```

应显示 `winapp` 状态 `✓ enabled`，54 tools。

### 4. 生效

需要 `/reset` 或重启 Hermes 会话。MCP 工具以 `mcp_winapp_` 前缀出现在工具列表中。

## 已知限制

- QWebEngine 内容（MiraBox Craft 等）UIA 树不可见，只能用截图
- 中文进程名 `attach_to_app` 匹配不稳定，用 `attach_to_pid` 代替
- 截图只截单个窗口，非全桌面

## 竞品对比（已放弃）

| | WinApp MCP | Screenhand |
|---|---|---|
| 选型原因 | Windows原生 .NET+FlaUI，锁屏可用，MIT | macOS主战场，AGPL-3.0，Windows知识库空 |
