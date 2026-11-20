# 我的技能清单（Skills）

> 用途：换机器时知道这台 DSH 有哪些技能可用、哪些是自带的、哪些要自己装。
> 记录时间：2026-11-20

## 通用技能

| 技能 | 来源 | 作用 |
|---|---|---|
| `find-skills` | 自装 | 发现并安装新技能；用户问"有没有能做 X 的技能"时用 |
| `diagnose-windows-sandbox-acl` | 内置 | 排查 Windows 沙箱权限被拒：检查路径及各级父目录 ACL 并修复 |

## Office 系列

| 技能 | 来源 | 作用 |
|---|---|---|
| `office` | 内置 | 总入口，处理 Office / PDF 时先加载，由它路由到下面几个 |
| `office-docx` | 内置 | Word（.docx）创建、读取、编辑、校验 |
| `office-pptx` | 内置 | PowerPoint（.pptx）创建、读取、编辑、校验 |
| `office-xlsx` | 内置 | Excel（.xlsx）创建、读取、编辑、校验，含公式 |
| `office-recalculate` | 内置 | 用 LibreOffice 重算表格并验证计算结果 |
| `office-render` | 内置 | 把文档渲染成图片，检查排版 |
| `office-export-pdf` | 内置 | Office 文档转 PDF |

## 文件位置

```
自装技能：<workspace>\.agents\skills\<技能名>\SKILL.md
内置技能：打包在 DSH 客户端里，随版本更新，不需要也不建议手动改
```

本机自装的那个：

```
C:\Users\Administrator\Documents\deepseek-harness\default-workspace\.agents\skills\find-skills\SKILL.md
```

## 怎么加新技能

1. 让 AI 用 `find-skills` 去生态里找现成的
2. 或者自己写一个 `SKILL.md`，放进 `<workspace>\.agents\skills\<名字>\`
3. 格式：开头用 YAML front matter 写 `name` 和 `description`，下面写正文

```markdown
---
name: my-skill
description: 一句话说清什么时候该用它
---

# My Skill

正文：什么时候用、怎么用、注意事项。
```

## 三层概念别混

| 层 | 是什么 | 例子 |
|---|---|---|
| 插件 | 扩展 DSH 客户端界面 | 侧边栏、插件市场、余额挂件 |
| 技能 | AI 干活时加载的说明书 | office 系列、find-skills |
| 工具 | AI 实际能调的函数 | 读写文件、跑命令、抓网页 |

## 已安装的第三方技能

| 技能 | 版本 | 来源 | 本地路径 |
|---|---|---|---|
| `a-stock-data` | V3.10.0 | https://github.com/simonlin1212/a-stock-data （Apache-2.0） | `.agents\skills\a-stock-data\` |

副本存于 skills/a-stock-data/（含 SKILL.md、LICENSE、SOURCE.md）。依赖：requests / mootdx / baostock / stockstats / xlrd / pandas / numpy / openpyxl。

| `uzi-skill` | V3.9.4 | https://github.com/wbh604/UZI-Skill （MIT） | `skills/uzi-skill/` |

