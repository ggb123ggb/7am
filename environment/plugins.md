# 我的 DSH 插件清单

> 用途：换机器、重装系统、或者哪天插件崩了，照这份清单一分钟恢复。
> 记录时间：2026-11-20

## 已装插件（插件市场）

| 插件 | 版本 | 作用 |
|---|---|---|
| `dshmarket` | 1.70.2 | 可视化插件市场：浏览、搜索、一键安装社区插件 |
| `dsh-better-sidebar` | 0.28.1 | 右侧边栏：文件树、编辑器、变更、任务、侧边聊天，每会话独立 |
| `dsh-context` | 0.77.0 | 上下文洞察：dashboard + `/context` 命令 |
| `dsh-whale-widget` | 0.4.2 | 右下角余额小鲸鱼挂件：余额、今日已用、峰谷定价、自定义气泡 |

## 官方基础组件

| 组件 | 作用 |
|---|---|
| `@deepseek-ai/dsh-base` | 核心 |
| `@deepseek-ai/dsh-web-app` | Web 界面 |
| `@deepseek-ai/dsh-experimental-auto-review` | 自动审查 |
| `@deepseek-ai/dsh-experimental-voice-input-bundle` | 语音输入 |

## 配置位置

```
C:\Users\Administrator\.dsh\profiles\desktop\package.json
```

关键字段是 `dependencies` 和 `dsh.profile.bundles`，两者必须同时存在——只加依赖不加 bundle，插件装了但不会加载。

## 恢复步骤（新机器）

1. 装好 DSH，找到 profile 目录：`%USERPROFILE%\.dsh\profiles\desktop\`
2. 把下面这段合并进该目录的 `package.json`：

```json
{
  "dependencies": {
    "dsh-better-sidebar": "0.28.1",
    "dsh-context": "0.77.0",
    "dsh-whale-widget": "0.4.2",
    "dshmarket": "^1.70.2"
  },
  "dsh": {
    "profile": {
      "bundles": [
        "@deepseek-ai/dsh-base",
        "@deepseek-ai/dsh-web-app",
        "@deepseek-ai/dsh-experimental-auto-review",
        "dshmarket",
        "dsh-better-sidebar",
        "dsh-context",
        "dsh-whale-widget",
        "@deepseek-ai/dsh-experimental-voice-input-bundle"
      ]
    }
  }
}
```

3. 在该目录执行 `pnpm install`
4. 重启 DSH

**更省事的办法**：装好 `dshmarket` 之后，在它的界面里按名字搜，一键装回来。

## 注意

- 插件版本别乱升。`dsh-context` 的 `package.json` 里写了兼容的 DSH 版本区间，升级前对一下
- `%USERPROFILE%\.dsh\` 下的 `speech-to-text`、`whale-audio`、`whale-roles`、`whale-bubble-imgs` 是插件的数据目录，删了会丢自定义配置（角色、音效、气泡图）
