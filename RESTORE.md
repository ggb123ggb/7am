# 换机器恢复指南（RESTORE）

> 目标：在一台陌生电脑上，10 分钟内把这份档案和技能恢复成可用状态。
> 适用于 Windows / macOS / Linux，命令差异处会标注。

---

## 0. 前提：装三样东西

| 工具 | 用途 | 说明 |
|---|---|---|
| Git | 拉仓库 | Windows: git-scm.com；macOS: `xcode-select --install` |
| Python 3.10+ | 跑技能脚本 | Windows 安装时勾选 **Add Python to PATH** |
| DSH（可选） | 恢复插件与 AI 客户端 | 不装也能用档案和技能 |

---

## 1. 拉仓库（私有仓库需要 Token）

**不要用账号密码。** 用 Fine-grained Personal Access Token：

1. GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens
2. Repository access 只选 `ggb123ggb/7am`
3. Permissions 只给 **Contents: Read-only**
4. 生成后立刻复制（只显示一次）

```bash
git clone https://github.com/ggb123ggb/7am.git
cd 7am
```

提示 `Password` 时粘贴 **token**。

拉完先确认：

```bash
git log --oneline -3
```

---

## 2. 装技能到本地

技能目录约定：**工作区**下的 `.agents/skills/<技能名>/`。

macOS / Linux：

```bash
mkdir -p ~/.agents/skills
cp -r skills/a-stock-data ~/.agents/skills/
cp -r skills/uzi-skill   ~/.agents/skills/
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.agents\skills" | Out-Null
Copy-Item skills\a-stock-data, skills\uzi-skill "$env:USERPROFILE\.agents\skills\" -Recurse -Force
```

---

## 3. 装 Python 依赖

```bash
# a-stock-data（轻量）
pip install requests pandas numpy mootdx baostock stockstats xlrd openpyxl

# uzi-skill（重，含 playwright）
cd skills/uzi-skill
pip install -r requirements.txt
playwright install chromium
cd ../..
```

> 国内网络 pip 慢的话加镜像：`-i https://pypi.tuna.tsinghua.edu.cn/simple`

---

## 4. 恢复 DSH 插件（可选）

把 `environment/plugins.md` 里那段 JSON 合并进新机器的：

```
%USERPROFILE%\.dsh\profiles\desktop\package.json
```

注意 **dependencies 和 dsh.profile.bundles 必须同时加**，只加依赖插件不会加载。然后：

```bash
cd %USERPROFILE%\.dsh\profiles\desktop
pnpm install
```

重启 DSH。

---

## 5. 验证

```bash
git log --oneline -3
python -c "import akshare; print(akshare.__version__)"
cd skills/uzi-skill && python run.py 600519 --depth lite --no-browser
```

最后一条能出 `reports/600519.SH_*/full-report.html` 就算全通了。

---

## 6. 陌生电脑的安全守则（重要）

1. **别让 Git 记住凭据**——公用电脑上等于把仓库送人：

```bash
git config --global credential.helper ""
```

2. **用完就撤销 token**：回 GitHub 对应页面点 Delete
3. **只读 token 就够了**，不要在陌生机器上 push
4. **别把仓库留在公用目录**，用完 `rm -rf 7am` 清掉
5. 仓库里有个人档案和持仓分析记录，注意别留在下载文件夹

---

## 7. 仓库里没有的东西（正常现象）

| 没有 | 原因 | 怎么办 |
|---|---|---|
| `node_modules/` | 体积大且会过期 | `pnpm install` 重装 |
| `.cache/`、`reports/` | 运行时生成 | 重新跑一次就有 |
| `venv/` | 与机器绑定 | `pip install -r requirements.txt` |

---

## 8. 一句话版本

```bash
git clone <repo> && cp -r skills/* ~/.agents/skills/ && pip install -r requirements.txt
```
