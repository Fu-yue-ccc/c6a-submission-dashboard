# C6A 教学说明

> 提交数据仪表盘 — 安装、运行、更新数据指南

---

## 一、快速开始（30 秒上手）

### 查看网站仪表盘

1. 打开 `C6A_Dashboard/dashboard/` 文件夹
2. **双击 `index.html`**，用浏览器（Chrome/Edge/Firefox）打开
3. 即可看到完整的提交数据仪表盘

> 不需要安装任何软件，不需要服务器，不需要联网（图表 CDN 需要联网加载）。

### 查看 Excel 报表

1. 打开 `C6A_Dashboard/report.xlsx`
2. 用 Excel / WPS / Numbers 打开
3. 包含 5 个 Sheet：总览、按学生、按挑战、时间线、缺失项

---

## 二、文件结构说明

```
C6A_Dashboard/
├── data/
│   ├── submissions.json      # 结构化提交数据（162条）
│   └── submissions.csv       # CSV 格式（可直接导入Excel）
├── dashboard/
│   └── index.html            # 交互式仪表盘网站（单文件）
├── screenshots/              # 运行截图（需自行补充）
│   └── README_截图说明.md
├── report.xlsx               # Excel 报表（5个Sheet）
├── generate_data.py          # 数据生成脚本
└── generate_excel.py         # Excel 生成脚本
```

---

## 三、网站功能使用指南

### 3.1 顶部统计卡片

页面顶部显示 4 个关键指标：
- 学生总数、挑战总数、整体完成率、缺失提交数

### 3.2 四个视图 Tab

| Tab | 说明 |
|-----|------|
| 📈 总览 | 3 个图表：状态分布饼图、各挑战完成率柱状图、学生完成率排名 |
| 🔲 提交矩阵 | 学生×挑战的彩色矩阵，绿色=完整，黄色=部分，红色=缺失 |
| 👤 按学生 | 学生列表，显示每人完成率和待完成项，可筛选 |
| 🎯 按挑战 | 挑战列表，显示每个挑战的完成情况，可筛选 |

### 3.3 查看详情

- **矩阵视图**：点击任意彩色格子，弹出该学生该挑战的详细信息（文件清单、提交时间、完成度）
- **学生视图**：点击学生卡片，弹出该学生全部提交记录
- **挑战视图**：点击挑战卡片，弹出该挑战全部学生的提交情况

### 3.4 筛选

- 按学生视图：顶部下拉菜单选择特定学生
- 按挑战视图：顶部下拉菜单选择特定挑战

---

## 四、更新数据

### 方法一：修改 JSON 后重新生成仪表盘

1. 编辑 `data/submissions.json`，添加/修改提交记录
2. 运行 `python3 generate_dashboard.py`（需将数据重新内嵌到 HTML）
3. 刷新浏览器

### 方法二：用脚本从文件夹自动扫描（扩展）

1. 修改 `generate_data.py`，将模拟数据替换为文件夹扫描逻辑
2. 运行 `python3 generate_data.py` 生成新的 JSON
3. 运行 `python3 generate_excel.py` 生成新的 Excel
4. 重新生成仪表盘 HTML

### 方法三：直接在 Excel 中修改

1. 打开 `report.xlsx`
2. 在"按学生"或"按挑战"Sheet 中直接修改
3. 保存即可

---

## 五、环境要求

| 用途 | 要求 |
|------|------|
| 查看仪表盘 | 任意现代浏览器（Chrome 90+ / Edge 90+ / Firefox 88+ / Safari 14+） |
| 查看 Excel | Excel 2016+ / WPS / Numbers / Google Sheets |
| 运行生成脚本 | Python 3.8+ + openpyxl（`pip install openpyxl`） |
| 网络 | 仪表盘图表需要联网加载 Tailwind 和 Chart.js CDN |

---

## 六、常见问题

### Q1：打开 HTML 后图表不显示？
A：检查网络连接，Tailwind CSS 和 Chart.js 通过 CDN 加载，需要联网。如果需要完全离线，可以将这两个库下载到本地并修改引用路径。

### Q2：怎么添加新的学生？
A：编辑 `submissions.json`，在 `students` 数组中添加新学生对象，然后在 `submissions` 数组中为该学生添加每个挑战的提交记录。

### Q3：怎么添加新的挑战？
A：编辑 `submissions.json`，在 `challenges` 对象中添加新挑战定义（含 required_files），然后为每个学生添加该挑战的提交记录。

### Q4：Excel 打开后颜色不显示？
A：确认使用的是 Excel 或 WPS，部分轻量级表格工具可能不支持条件格式。

### Q5：仪表盘可以部署到网上吗？
A：可以。将 `dashboard/index.html` 推送到 GitHub，启用 GitHub Pages，或拖拽到 Netlify，即可获得公网链接。

---

## 七、扩展到真实班级数据

当前数据为模拟数据（18 人 × 9 挑战）。要使用真实数据：

1. **收集文件**：将全班提交文件整理到一个文件夹，按 `姓名拼音_挑战编号_文件名` 规范命名
2. **扫描生成**：修改 `generate_data.py`，用 `os.walk` 扫描文件夹，用正则匹配文件名
3. **自动判定**：对照每个挑战的 `required_files`，自动判定每个提交的状态
4. **生成报表**：运行 `generate_excel.py` 生成 Excel，运行 `generate_dashboard.py` 生成网站
