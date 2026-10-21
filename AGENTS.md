# AGENTS.md · 给 AI 编程助手看的仓库说明

## 项目是什么

Coffee Cost Lab（杯杯有数）是一个**纯前端单页应用**：零依赖、零构建、单文件。
整个应用就是根目录的 `index.html`（HTML + 内联 CSS + 内联 `<script>`），用浏览器打开即用。

功能模块（都在 `index.html` 里）：
- **原料库** —— `addIngredient()` / `delIngredient()` / `fillPresets()` / `renderIngredients()`
- **饮品配方** —— `addDrink()` / `delDrink()` / `selectDrink()` / `onDrinkField()` / `onRowIng()` / `onRowAmount()` / `renderDrinks()`
- **菜单总览** —— `renderOverview()`
- **定价建议与保本** —— `onMarginInput()` / `onFixedInput()` / `renderPricing()` / `renderBreakeven()`

## 数据模型

```js
state = {
  ingredients: [{ id, name, unit: 'g'|'ml'|'个', specQty, price }],
  drinks:      [{ id, name, price, items: [{ ingId, amount }] }],
  fixed:       { rent, labor, util, other },   // 月固定成本（元）
  targetMargin: 70                            // 目标毛利率（%）
}
```

- 持久化：`localStorage`，键名 `ccl-data-v1`；首次打开无数据时用 `seed()` 填入示例
- 纯计算函数：`unitCost()` / `drinkCost()` / `drinkMargin()` / `suggestedPrice()` / `monthlyFixed()` / `avgMarginPerCup()`
- 删除原料会级联移除引用它的配方用量（见 `delIngredient()`）

## 开发约定

1. **保持单文件**：不要引入构建工具、框架或 npm 依赖——"双击打开就能用"是核心卖点。
2. **中文界面文案**：简体中文，面向咖啡馆老板/咖啡师，语气实在、口语化；数字用 `money()` / `pct()` 格式化。
3. **移动端验证**：改完检查 375px 宽度下表格和表单不错乱。
4. **不要破坏性变更 localStorage 结构**：`ccl-data-v1` 的字段只增不改；真要改结构必须写迁移逻辑。
5. **用户输入要做防护**：金额/数量用 `parseFloat(...) || 0` 兜底，`esc()` 转义后才插入 HTML。
6. **计算口径变更要在 README「计算逻辑」一节同步更新**。

## 怎么跑 / 怎么测

```bash
python -m http.server 8000   # 然后浏览器打开 http://localhost:8000
```

提交前自查：
- [ ] 原料增删、配方增删改、定价、保本全流程走一遍
- [ ] 375px 移动端布局正常
- [ ] JS 无语法错误（CI 会自动跑 `node --check`）
- [ ] 刷新页面后数据还在（localStorage 持久化正常）
