# 千问 Vision 辅助协议 (Qianwen)

> 角色：vision/OCR 辅助工具，不接入协作路由
> 通道：桌面截图 + G先生中转
> 状态：🔭 辅助工具

## 用途

千问(Qwen3.7)桌面客户端用作 vision 辅助——看截图、报坐标、分析页面结构。

**不接 API、不配端口、不走路由。** 走 G先生人工中转。

## 典型工作流

```
1. 小茉截图 → 存桌面 for_qianwen.png
2. G先生打开千问 → 上传截图 → 问"找输入框坐标"
3. 千问回报像素坐标
4. 小茉 click_at_coordinates(x, y) → 精准点击
```

## ⚠️ 注意

**Hermes 内部不可配属 vision API provider。** 会导致启动崩溃。只走桌面客户端文件路由。

## 目标特征

- 路径: `%LOCALAPPDATA%\Programs\QianwenApp\qianwen.exe`
- 版本: 3.5.2 / 3.7 模型
- 窗口标题: "千问"
- 无端口、无 API、纯桌面客户端
