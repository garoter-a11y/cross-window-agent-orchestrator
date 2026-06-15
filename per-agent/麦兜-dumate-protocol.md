# 麦兜通信协议 (DuMate)

> 通道：文件 inbox 双向读写
> 读取：`read_file` 从 inbox 取回复
> 状态：✅ 文件双向通（需定时任务扫 inbox）

## 通信原理

DuMate 的聊天输入框是 web 编辑器（contentEditable div），UIA 无法穿透。改用文件 inbox 作为通信通道。

```
小茉写 → inbox/小茉_msg_N.md → 麦兜定时扫 inbox → 读取 → 回复
麦兜回 → inbox/麦兜_reply_N.md → 小茉 read_file → 读取回复
```

## 发送消息

```python
# 写入 inbox
write_file(
    path="C:/Users/Administrator/.qianfan/workspace/<id>/.dumate/inbox/小茉_msg_001.md",
    content="麦兜，帮我审查..."
)
```

## 读取回复

```python
# 读 inbox 目录
ls "C:/Users/Administrator/.qianfan/workspace/<id>/.dumate/inbox/"

# 读回复文件
read_file("C:/Users/Administrator/.qianfan/workspace/<id>/.dumate/inbox/麦兜_reply_001.md")
```

## 麦兜侧 skill

已安装到 DuMate 的 skills 目录：
`C:/Users/Administrator/AppData/Local/Programs/DuMate/resources/extra-resource/opencode/skills/小茉路由/SKILL.md`

麦兜回复格式：
```yaml
---
from: 麦兜
to: 小茉莉
timestamp: 2026-06-16T04:44:54
type: reply
in_reply_to: 小茉_msg_001.md
---
回复内容...
```

## 触发方式

麦兜需手动或定时任务触发："检查小茉消息"或"扫描 inbox 目录"。建议建 DuMate 定时任务每分钟扫一次。

## 目标特征

- 进程: DuMate (PID变化，需 attach_to_pid)
- 输入: web编辑器（UIA盲区），坐标粘贴无效
- 通信: inbox 文件目录
- 模型: 百度千帆
