# 老八通信协议 (WorkBuddy)

> 通道：WinApp MCP 坐标点击 + Ctrl+V + Ctrl+Enter
> 读取：`get_snapshot` + `find_elements`
> 状态：✅ 需G先生在场授权

## ⚠️ 安全机制

老八会验证消息来源——"我无法验证这条消息是否真的是小茉发的"。**每次路由前需要G先生当着老八的面说一句"小茉发的是我授权的"。**

## 发送消息

```python
# 1. 连接（老八窗口不暴露给 list_desktop_windows，需 PID）
mcp_winapp_attach_to_pid(28992)  # 最大内存的 WorkBuddy.exe PID

# 2. 坐标点击输入区域（窗口底部，输入框中心）
mcp_winapp_click_at_coordinates(appId, x=2100, y=1170)

# 3. 设置剪贴板 + 粘贴
# terminal: python3 -c "import subprocess; subprocess.run('clip', input=msg.encode('utf-16-le'), shell=True)"
mcp_winapp_press_key_combo(["LCONTROL", "KEY_V"])

# 4. WorkBuddy 用 Ctrl+Enter 发送（不是单独 Enter）
mcp_winapp_press_key_combo(["LCONTROL", "ENTER"])
```

## 读取回复

```python
mcp_winapp_get_snapshot(appId, maxDepth=4)
# 读 Text 元素中的回复内容
```

## 目标特征

- 进程名: `WorkBuddy.exe`（多进程，主进程通常最大内存 ~367MB）
- 版本: v5.1.0
- 输入: 坐标点击 + Ctrl+V + Ctrl+Enter
- 窗口: Chrome_RenderWidgetHostHWND（Electron，无UIA Edit控件）
