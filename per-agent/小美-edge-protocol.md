# 小美通信协议 (OpenClaw/Edge)

> 通道：WinApp MCP `type_text` → Edge 输入框 → ENTER
> 读取：`get_snapshot` + `find_elements`
> 状态：✅ 全自动双向通

## 发送消息

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
# 搜索回复内容
mcp_winapp_find_elements(appId, nameContains="关键词")
```

## 目标特征

- 进程名: `msedge`
- 标签页: "OpenClaw Control"
- 模型: DeepSeek V4 Flash
- Edge 版本: v2026.6.6
