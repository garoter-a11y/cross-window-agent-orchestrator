# 扣子通信协议 (Coze)

> 通道：桌面文件 + Shell 白名单（cat/echo）
> 读取：`read_file` 读桌面回复文件
> 状态：✅ 文件双向通（需G先生传话触发）

## 通信原理

扣子有 Shell 白名单（echo/cat/dir/ls 等），通过桌面文件通信：

```
小茉写 → 桌面文件 → G先生对扣子说"cat xxx" → 扣子读取
扣子回 → echo 到桌面回复文件 → 小茉 read_file
```

## 发送消息

```python
# 写入桌面
write_file(
    path="C:/Users/Administrator/Desktop/xiaomo_to_kouzi.txt",
    content="扣子，帮我..."
)
# G先生对扣子说：cat C:\Users\Administrator\Desktop\xiaomo_to_kouzi.txt
```

## 读取回复

```python
read_file("C:/Users/Administrator/Desktop/kouzi_reply.txt")
```

## 目标特征

- 进程: `扣子，你的 AI 办公助手` PID变化
- 模型: 豆包 2.0-pro
- 输入: web编辑器（UIA盲区）
- Shell白名单: echo, write-output, dir, ls, cat, type, findstr等
- 自带文件: 可在桌面上传/下载文件
