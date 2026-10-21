# 🧮 Coffee Cost Lab · 杯杯有数

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![CI](https://github.com/divid0407/coffee-cost-lab/actions/workflows/ci.yml/badge.svg)](https://github.com/divid0407/coffee-cost-lab/actions/workflows/ci.yml)
[![GitHub Pages](https://github.com/divid0407/coffee-cost-lab/actions/workflows/pages.yml/badge.svg)](https://github.com/divid0407/coffee-cost-lab/actions/workflows/pages.yml)

**给咖啡馆老板的饮品成本核算工具**：原料库、配方成本、定价建议、保本测算，一页搞定。

> 🎯 **在线使用**：<https://divid0407.github.io/coffee-cost-lab/>（需在仓库 Settings → Pages 启用 GitHub Pages 后生效）

开一家咖啡馆，最扎心的问题往往不是"好不好喝"，而是"这一杯到底赚不赚钱"。
这个工具帮你把每杯饮品的原料成本算清楚，按目标毛利率反推定价，再算出每天卖多少杯才能保本。

## ✨ 功能

- **原料库**：录入原料规格和进货价，自动算出单位成本（元/g、元/ml、元/个）；一键填入常用原料示例
- **饮品配方**：给每杯饮品列原料用量，实时算出单杯原料成本、毛利率、单杯毛利
- **菜单总览**：所有饮品的成本与毛利一览，毛利率偏低的自动标红提醒
- **定价建议**：设定目标毛利率，按"售价 = 成本 ÷ (1 − 毛利率)"反推建议售价
- **保本测算**：填月固定成本（房租/人工/水电），算出日保本杯数

纯前端单页应用，零依赖、零构建，数据只存在本机浏览器（localStorage），不上传。

## 🚀 快速开始

```bash
# 直接用浏览器打开
open index.html        # macOS
start index.html       # Windows
```

或者起一个本地服务：

```bash
python -m http.server 8000
```

## 🧮 计算逻辑

- **单位成本** = 进货价 ÷ 规格数量
- **单杯原料成本** = Σ(用量 × 单位成本)
- **毛利率** = (售价 − 成本) ÷ 售价
- **建议售价** = 成本 ÷ (1 − 目标毛利率)
- **日保本杯数** = 日均固定成本 ÷ 平均单杯毛利（简化模型，未计外卖抽成、损耗与销量权重，仅供快速估算）

## 🗺 路线图

- [x] 原料库 / 饮品配方 / 菜单总览 / 定价建议 / 保本测算
- [ ] 饮品销量权重（按实际销量算加权保本点）
- [ ] 配方一键导出图片（发给合伙人看）
- [ ] 英文界面切换

## 🤝 贡献

如果你开咖啡馆、做咖啡师，欢迎按你的吧台经验提 Issue 纠正默认参数！
先看看 [CONTRIBUTING.md](./CONTRIBUTING.md)，AI 编程助手请先读 [AGENTS.md](./AGENTS.md)。

## 📄 License

[MIT](./LICENSE)
