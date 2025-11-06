# 作弊菜单 - 使用指南

## 快速开始

### 文件清单
已在 `in_game/common/` 目录创建以下文件：

1. **scripted_guis/cheat_menu_scripted_guis.txt**
   - 35 个按钮的脚本 GUI 定义
   - 按钮名称: `cheat_xxx_button`
   - 执行相应的游戏效果

2. **scripted_effects/cheat_menu_modifiers_effects.txt**
   - 4 个修改器定义
   - 7 个触发条件
   - 1 个月度效果处理

## 按钮名称参考

### 经济
- `cheat_add_gold_button`
- `cheat_add_manpower_button`
- `cheat_add_sailors_button`

### 稳定性
- `cheat_max_stability_button`
- `cheat_add_stability_button`
- `cheat_max_legitimacy_button`
- `cheat_add_prestige_button`

### 军事
- `cheat_max_professionalism_button`
- `cheat_add_army_tradition_button`
- `cheat_add_navy_tradition_button`

### 政府
- `cheat_add_republican_tradition_button`
- `cheat_add_devotion_button`
- `cheat_add_horde_unity_button`
- `cheat_add_reform_progress_button`
- `cheat_max_absolutism_button`

### 宗教
- `cheat_add_karma_button`
- `cheat_add_harmony_button`
- `cheat_add_doom_button`

### 研究
- `cheat_toggle_research_speed_button`
- `cheat_add_literacy_button`

### 增益
- `cheat_toggle_super_nation_button`
- `cheat_toggle_instant_construction_button`
- `cheat_toggle_fast_recruitment_button`
- `cheat_toggle_reduced_unrest_button`

### 地图
- `cheat_discover_all_provinces_button`
- `cheat_lift_fog_of_war_button`

### 省份
- `cheat_change_culture_button`
- `cheat_change_religion_button`

### 其他
- `cheat_reduce_war_exhaustion_button`
- `cheat_reduce_corruption_button`
- `cheat_add_mercantilism_button`
- `cheat_add_innovativeness_button`
- `cheat_reduce_inflation_button`

## 在 GUI 中使用

在 `cheat_menu_window.gui` 中，按钮的 `onclick` 应该这样写：

```
onclick = "[GetScriptedGui('cheat_add_gold_button').Execute(GuiScope.SetRoot(GetPlayer.MakeScope).End)]"
```

## 修改器列表

启用的增益会自动应用以下修改器：

1. **cheat_super_nation_modifier**
   - 建造成本 -50%
   - 招募成本 -50%
   - 士气 +50%
   - 伤害 +50%

2. **cheat_instant_construction_modifier**
   - 建造成本 -99%
   - 建造时间 -99%

3. **cheat_fast_recruitment_modifier**
   - 招募成本 -90%
   - 招募时间 -90%

4. **cheat_reduced_unrest_modifier**
   - 全国动乱 -2
   - 本地动乱 -2

## 触发条件

可在条件判断中使用：

- `cheat_is_super_nation_enabled`
- `cheat_is_instant_construction_enabled`
- `cheat_is_fast_recruitment_enabled`
- `cheat_is_reduced_unrest_enabled`
- `cheat_is_research_speed_enabled`
- `cheat_is_player_country`
- `cheat_can_use_cheats`

## 常见问题

### Q: 按钮为什么没有反应？
A: 检查 GUI 中的 ScriptedGui 名称是否完全匹配，确保 mod 已启用。

### Q: 修改器没有显示？
A: 确保 `cheat_menu_modifiers_effects.txt` 已加载，修改器有 1200 天（20 年）的期限。

### Q: 如何自定义效果值？
A: 编辑 `cheat_menu_scripted_guis.txt` 中对应按钮的 `on_select` 部分，修改效果的参数值。

### Q: 可以添加新按钮吗？
A: 可以。复制现有按钮的格式，使用新的按钮名称并定义相应的效果。

## 技术说明

### 作用域
所有按钮都使用 `country` 作用域，通过 `GuiScope.SetRoot(GetPlayer.MakeScope)` 获取玩家国家。

### 变量系统
切换类按钮使用脚本变量来管理状态：
- `cheat_research_speed_enabled`
- `cheat_super_nation_enabled`
- `cheat_instant_construction_enabled`
- `cheat_fast_recruitment_enabled`
- `cheat_reduced_unrest_enabled`

### 月度处理
修改器通过 `cheat_apply_monthly_effects` 脚本在每个月自动应用，自动续期 1200 天。

## 文件位置

```
in_game/common/
├── scripted_guis/
│   └── cheat_menu_scripted_guis.txt
└── scripted_effects/
    └── cheat_menu_modifiers_effects.txt
```

## 相关文档

- `IMPLEMENTATION_SUMMARY.md` - 详细实现说明
- `QUICK_REFERENCE.md` - 快速参考指南
- `FORMAT_FIX_REPORT.md` - 格式修正详情
- `IMPLEMENTATION_REPORT.md` - 项目报告
- `COMPLETION_SUMMARY.md` - 完成总结

---

**版本**: 1.0.0  
**最后更新**: 2025年11月6日
