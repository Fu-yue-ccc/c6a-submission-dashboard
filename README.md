# C6A 提交数据仪表盘（Submission Data Dashboard）

把班级 18 位同学 × 9 个挑战的提交数据，做成**自动生成 + 可交互查看**的数据仪表盘。

## 交付内容

| 路径 | 说明 |
| --- | --- |
| `data/submissions.json` | 结构化数据源（每人的每个挑战：已完成 / 部分完成 / 缺失） |
| `data/submissions.csv` | 同上的 CSV 版本，便于 Excel / pandas 直接读取 |
| `dashboard/index.html` | 仪表盘前端（Tailwind + Chart.js，单文件，数据内嵌，双击即可打开） |
| `report.xlsx` | 自动生成的 Excel 报表，5 个 Sheet，缺失明细行标红 |
| `generate_excel.py` | 自动化脚本：从 `data/submissions.json` 生成 `report.xlsx` |
| `方案设计.md` | 设计思路、指标体系与数据口径 |
| `教学说明.md` | 给老师的运行/复现说明 |
| `AI_LOG.md` | AI 使用记录 |
| `拿来说明.md` | 交付物说明与验收对照 |
| `AAR.md` | 七维 AAR 复盘 |

## 数据快照

- 覆盖 **18 位同学 / 4 个专业 / 9 个挑战**（C2、C4A、C4B、C4C、C4D、C5、C5A、C6、C6A）
- 共 162 个「学生 × 挑战」单元：**已完成 75、部分完成 24、缺失 63**（完成率 46.3%）
- `report.xlsx` 的缺失明细 Sheet 共 **87 行**，按状态条件格式标红

## 使用方式

1. 打开仪表盘：直接双击 `dashboard/index.html`，或本地起服务
   ```bash
   python3 -m http.server 8080
   # 浏览器打开 http://localhost:8080/dashboard/index.html
   ```
2. 重新生成报表：
   ```bash
   pip install openpyxl
   python3 generate_excel.py     # 读取 data/submissions.json → 输出 report.xlsx
   ```

## 可复用性

数据与展示分离：更新 `data/submissions.json` 后重跑 `generate_excel.py` 即可刷新报表；
该脚本只用 `openpyxl` 一个依赖，换一份名单/挑战清单也能直接复用。
