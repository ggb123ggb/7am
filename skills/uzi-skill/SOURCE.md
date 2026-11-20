# UZI-Skill

- 来源：https://github.com/wbh604/UZI-Skill
- 作者：FloatFu-true
- 版本：3.9.4
- 许可证：MIT（见同目录 LICENSE）
- 用途：A股/港股/美股个股深度分析，22 维数据 × 66 投资人评委 × 机构建模 → HTML 报告

第三方技能副本，仅作备份与跨设备同步。升级以原仓库为准：

```
git clone https://github.com/wbh604/UZI-Skill
```

## 运行

```bash
pip install -r requirements.txt
python run.py 600519 --depth lite --no-browser
```

## 实测记录（2026-11-20）

- Python 3.12.14 + akshare 1.20.65，lite 档跑 600519 成功
- 综合 59.6/100，观望中性，风格识别「白马价值」
- 数据覆盖 89%；5 个维度（宏观/行业/原材料/期货/政策）兜底失败，需 Playwright 或 MX_APIKEY 补
- 未装 Playwright，PNG 图表未生成（不影响 HTML）
- 覆盖率生成物（.cache/、reports/）已排除，不随仓库分发
