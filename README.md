# 个人档案 · 使用说明

一套跨工具、跨设备的"我是谁"说明书。核心只有一件事：**让 AI 不用每次都重新认识你**。

## 结构

```
7am/
├── SKILL.md              个人档案主文件，AI 读这个
├── RESTORE.md            换机器恢复指南（先看这个）
├── README.md             本文件
├── CHANGELOG.md          改动记录
├── environment/
│   ├── plugins.md        DSH 插件清单 + 恢复步骤
│   ├── plugins.json
│   ├── skills.md         技能清单（自装 / 内置 / 第三方）
│   └── skills.json
├── projects/
│   └── _template.md      单个项目的记录模板
├── skills/               归档的第三方技能副本
│   ├── a-stock-data/     A股数据接口（Apache-2.0）
│   └── uzi-skill/        个股分析报告（MIT）
└── .gitignore
```

## 三种用法

**1. 本地工具（Codex / 终端类）**

把仓库放在固定路径，每次开工先说：

```
读 <路径>/SKILL.md，按里面的偏好来
```

**2. 云端对话（网页版模型）**

把 `SKILL.md` 全文粘进对话开头，或作为附件上传。文件才几 KB，不占多少上下文。

**3. 多设备**

```bash
git add .
git commit -m "更新档案：xxx"
git push
```

换电脑 `git clone` 下来即可，完整步骤见 [RESTORE.md](RESTORE.md)。Git 自带修改记录，等于给档案留了时间轴。

## 什么时候更新

只有四种情况值得写：完成一个节点、被纠正一次、提出新偏好、同一个坑踩第二次。

判断标准很简单——**下次不写，我会不会又解释一遍？** 会，就写。

## 维护建议

- 每周花五分钟扫一眼，删掉过时的条目。档案变肥不是好事，上下文是有成本的
- 敏感信息（身份证、密码、客户名）不要写进来，尤其推到 GitHub 之前
- 私有仓库记得设为 Private
- 第三方技能（`skills/` 下）保留 LICENSE 和 `SOURCE.md`，升级以原仓库为准

## 环境清单

`environment/plugins.md` 记录这台机器装的 DSH 插件和版本，换机器时照着恢复。

`environment/skills.md` 记录可用的技能，以及自装、内置、第三方三种来源的区别。

## 换机器

直接看 [RESTORE.md](RESTORE.md)：拉仓库 → 装技能 → 装依赖 → 恢复插件，四步。
