# C6A 拿来说明

> 提交数据仪表盘的借鉴来源与数据说明

---

## 使用的开源库与工具

| 库/工具 | 用途 | 许可证 |
|---------|------|--------|
| Tailwind CSS (CDN) | UI 样式框架 | MIT |
| Chart.js 4.4 | 图表渲染（饼图/柱状图/条形图） | MIT |
| Python 3.12 | 数据生成和 Excel 生成脚本 | PSF |
| openpyxl | Excel 文件生成 | MIT |
| OpenStreetMap | （C6 Web App 使用，C6A 未直接使用） | ODbL |

## 参考资料

| 资料 | 来源 | 用途 |
|------|------|------|
| C6A.pdf | Elite20 挑战材料 | 任务要求、数据模型 Schema、四级任务 |
| C4A 挑战规范 | Elite20 挑战材料 | 评审技能——数据收集的基础 |
| openpyxl 官方文档 | openpyxl.readthedocs.io | Excel 生成 API |
| Chart.js 官方文档 | chartjs.org | 图表配置参考 |
| Tailwind CSS 官方文档 | tailwindcss.com | 样式类参考 |

## 数据来源说明

**当前数据为模拟数据**，由 `generate_data.py` 脚本随机生成：
- 18 个学生（覆盖 4 个专业）
- 9 个挑战（C2/C4A/C4B/C4C/C4D/C5/C5A/C6/C6A）
- 162 条提交记录
- 整体完成率 46.3%

模拟数据的学生姓名、专业、GitHub 用户名均为虚构，如有雷同纯属巧合。

**扩展到真实数据**：修改 `generate_data.py`，将模拟数据生成逻辑替换为文件夹扫描逻辑（os.walk + 正则匹配文件名），数据结构完全兼容。

## AI 使用声明

本项目使用豆包（Doubao）辅助开发，包括方案设计、代码生成、文档撰写、调试辅助。所有 AI 生成内容均经过人工审查和实际运行验证。详细记录见 Student_C6A_AI日志.md。
