# 顺手 · 动作市场（bazaar）

给「顺手」（会看场合的网页工具）用的**动作包目录**：这里只放**配置数据，没有代码**。

- **动作** = 内置能力 + 参数（数据）
- **变量组** = 声明式提取规则（数据）
- **AI 提取器** = 提示词（数据）
- **密钥永不出现**：包里的连接参数是空的，安装方自己绑（同类连接唯一时自动绑定）

## 在顺手里安装

配置台 →「**市场**」页 → 默认源就是本仓库的 `index.json` → 选一个动作包 → 安装（新场景 / 并入「始终出现」层）。

也可以手动：下载任一 `packs/*.action-pack.json`，在配置台「场景」页 →「⬆ 导入动作包」粘贴。

## 目录结构

```
index.json                     动作包列表（schemaVersion 1）
packs/*.action-pack.json       动作包本体
```

## 贡献一个动作包

1. 在顺手配置台里把场景导出成 `.action-pack.json`（场景页 → 底部「动作包 → 导出…」）；
2. 把文件放进 `packs/`，在 `index.json` 的 `items` 里加一条（`id` 用文件名，`path` 用相对路径）；
3. 发 PR。

要求：

- **不含密钥 / 个人连接信息**（导出时连接参数已自动清空）；
- 只引用**内置能力**（在「添加动作」里能搜到的能力 id）；
- 说明里写清楚需要什么连接（如「需要一个 AI 模型连接」）。

## 格式

`index.json`：

```jsonc
{
  "schemaVersion": 1,
  "updatedAt": "2026-09-13",
  "items": [
    {
      "id": "ai-tweet",
      "name": "AI 总结与分享",
      "description": "一句话说明",
      "author": "养恐龙",
      "version": "1.0.0",
      "path": "packs/ai-tweet.action-pack.json"
    }
  ]
}
```

动作包（`.action-pack.json`，由顺手导出）：

```jsonc
{
  "kind": "shunshou.action-pack",
  "schemaVersion": 1,
  "name": "场景名",
  "requires": {
    "capabilities": ["share.intent"],                 // 缺失时安装后动作会被禁用并说明
    "connections": [{ "kind": "llm", "label": "AI 模型（OpenAI 兼容）" }]
  },
  "provides": {
    "scene": { "id": "...", "name": "...", "match": {}, "tree": [] },
    "fieldGroups": [/* 可选：被引用的变量组 */],
    "aiExtractors": [/* 可选：被引用的 AI 提取器 */]
  }
}
```
