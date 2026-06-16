# 小美通信协议 (OpenClaw)

> 通道A（主力）：WebChat 直连 — Hermes 与 OpenClaw WebChat 直接通信，无需过 Edge
> 通道B（兜底）：WinApp MCP `type_text` → Edge 输入框 → ENTER
> 状态：✅ 全自动双向通

## 通道A：WebChat 直连（推荐）

当 OpenClaw 以 WebChat 模式运行时，小茉（Hermes）可通过内置消息路由直接与小美通信，无需经过桌面输入框。

适用场景：OpenClaw WebChat 窗口已打开，两者在同一上下文。

> 注：此通道不依赖 `msedge` 进程和 WinApp MCP 的 `type_text`，架构允许 Agent 间直连。

## 通道B：Edge 输入框（兜底）

```python
# 1. 锁定 Edge 窗口
mcp_winapp_attach_to_app("msedge")

# 2. 找到输入框
mcp_winapp_find_elements(appId, controlType="Edit", nameContains="发送")

# 3. 打字
mcp_winapp_type_text(appId, name="给 Assistant 发消息（Enter 发送）", text="消息内容")

# 4. 发送
mcp_winapp_press_key("RETURN")
```

## 读取回复

```python
mcp_winapp_find_elements(appId, nameContains="关键词")
```

## 目标特征

- 进程名: `msedge`
- 标签页: "OpenClaw Control"
- 模型: DeepSeek V4 Flash
- Edge 版本: v2026.6.6
