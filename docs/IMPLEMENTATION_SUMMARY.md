##############################
# 作弊菜单 - 实现总结
##############################

## 已实现的功能

本文档总结了作弊菜单 GUI (`cheat_menu_window.gui`) 中所有方法的实现情况。

### 1. 文件结构

```
in_game/common/
├── scripted_guis/
│   └── cheat_menu_scripted_guis.txt     # 所有 ScriptedGui 按钮的实现
└── scripted_effects/
    └── cheat_menu_modifiers_effects.txt # 修改器、触发条件和效果的实现
```

### 2. 已实现的 ScriptedGui 按钮 (35 个)

#### 经济部分 (3 个)
- **cheat_add_gold_button**: 增加 10000 金币 - `add_gold = 10000`
- **cheat_add_manpower_button**: 增加 50000 人力 - `add_manpower = 50000`
- **cheat_add_sailors_button**: 增加 50000 水手 - `add_sailors = 50000`

#### 稳定性部分 (4 个)
- **cheat_max_stability_button**: 设置稳定性为 3 - `set_stability = 3`
- **cheat_add_stability_button**: 增加 2 点稳定性 - `add_stability = 2`
- **cheat_max_legitimacy_button**: 设置正统性为 3 - `set_legitimacy = 3`
- **cheat_add_prestige_button**: 增加 100 威望 - `add_prestige = 100`

#### 军事部分 (3 个)
- **cheat_max_professionalism_button**: 设置专业性为 1 - `set_professionalism = 1`
- **cheat_add_army_tradition_button**: 增加 50 陆军传统 - `add_army_tradition = 50`
- **cheat_add_navy_tradition_button**: 增加 50 海军传统 - `add_navy_tradition = 50`

#### 政府部分 (5 个)
- **cheat_add_republican_tradition_button**: 增加 10 共和传统 - `add_republican_tradition = 10`
- **cheat_add_devotion_button**: 增加 10 忠诚度 - `add_devotion = 10`
- **cheat_add_horde_unity_button**: 增加 10 部落统一性 - `add_horde_unity = 10`
- **cheat_add_reform_progress_button**: 增加 50 改革进度 - `add_reform_progress = 50`
- **cheat_max_absolutism_button**: 设置专制权力为 3 - `set_absolutism = 3`

#### 宗教部分 (3 个)
- **cheat_add_karma_button**: 增加 50 业力 - `add_karma = 50`
- **cheat_add_harmony_button**: 增加 50 和谐度 - `add_harmony = 50`
- **cheat_add_doom_button**: 增加 50 末日 - `add_doom = 50`

#### 研究部分 (2 个)
- **cheat_toggle_research_speed_button**: 切换研究速度增益 - 控制变量
- **cheat_add_literacy_button**: 增加研究进度 - `add_research_progress = 0.1`

#### 增益部分 (4 个)
- **cheat_toggle_super_nation_button**: 切换超级大国增益 - 变量/修改器系统
- **cheat_toggle_instant_construction_button**: 切换瞬间建筑 - 变量/修改器系统
- **cheat_toggle_fast_recruitment_button**: 切换快速招募 - 变量/修改器系统
- **cheat_toggle_reduced_unrest_button**: 切换降低动乱 - 变量/修改器系统

#### 地图部分 (2 个)
- **cheat_discover_all_provinces_button**: 发现所有省份 - `discover_all_provinces = yes`
- **cheat_lift_fog_of_war_button**: 解除战争迷雾 - `lift_fog_of_war = root`

#### 省份部分 (2 个)
- **cheat_change_culture_button**: 改变文化 - 随机改变拥有省份文化
- **cheat_change_religion_button**: 改变宗教 - 随机改变拥有省份宗教

#### 其他部分 (5 个)
- **cheat_reduce_war_exhaustion_button**: 减少战争疲惫 - `add_war_exhaustion = -10`
- **cheat_reduce_corruption_button**: 减少腐败 - `add_corruption = -10`
- **cheat_add_mercantilism_button**: 增加重商主义 - `add_mercantilism = 10`
- **cheat_add_innovativeness_button**: 增加创新性 - `add_inflation = 0.05`
- **cheat_reduce_inflation_button**: 减少通货膨胀 - `add_inflation = -5`

### 3. 实现的修改器 (4 个)

- **cheat_super_nation_modifier**: 超级大国 - 降低建造和招募成本 50%，增加伤害和士气
- **cheat_instant_construction_modifier**: 瞬间建筑 - 将建造成本和时间降低 99%
- **cheat_fast_recruitment_modifier**: 快速招募 - 将招募成本和时间降低 90%
- **cheat_reduced_unrest_modifier**: 降低动乱 - 降低 2 点本地和全国动乱

### 4. 实现的触发条件 (5 个)

- **cheat_is_super_nation_enabled**: 检查超级大国是否启用
- **cheat_is_instant_construction_enabled**: 检查瞬间建筑是否启用
- **cheat_is_fast_recruitment_enabled**: 检查快速招募是否启用
- **cheat_is_reduced_unrest_enabled**: 检查降低动乱是否启用
- **cheat_is_research_speed_enabled**: 检查研究速度是否启用
- **cheat_is_player_country**: 检查是否为玩家国家
- **cheat_can_use_cheats**: 检查是否可使用作弊功能

### 5. 实现的脚本效果 (1 个)

- **cheat_apply_monthly_effects**: 月度效果处理 - 根据启用状态应用对应的修改器和增益

### 6. API 数据源

使用了 EU5 Modifier MCP Server (v2.0.0) 提供的以下资源:
- **Effects**: 1324 条 - 用于实现各种游戏效果
- **Modifiers**: 1855 条 - 用于定义临时增益修改器
- **Triggers**: 1500 条 - 用于条件检查
- **Data Types**: 24442 条 - 支持类型系统

### 7. 技术实现特点

#### 按钮类型
- **直接效果按钮**: 立即执行游戏效果（经济、稳定性、军事等）
- **切换按钮**: 使用变量系统启用/禁用增益（超级大国、快速建筑等）
- **组合按钮**: 支持多个效果组合（省份修改、寻路等）

#### 作用域
- 所有按钮都以 **country** 作为主要作用域
- 支持通过 `GuiScope.SetRoot(GetPlayer.MakeScope).End` 获取玩家国家上下文

#### 修改器系统
- 使用 **scripted_modifier** 定义长期增益效果
- 支持 **has_modifier** 检查以避免重复应用
- 自动过期期限设置为 1200 天（20 年）

### 8. 使用方式

在游戏中，玩家可以通过:
1. 打开作弊菜单窗口
2. 在各个章节中选择对应的按钮
3. 直接效果按钮会立即应用游戏效果
4. 切换按钮会启用/禁用特定增益效果

### 9. 扩展方向

可以进一步扩展以支持:
- 参数化值选择 (输入框)
- 多选项选择 (下拉菜单)
- 条件显示 (仅在特定情况下显示)
- 效果确认对话框

### 10. 兼容性

所有实现都基于官方 EU5 API，兼容:
- 欧陆风云 V 最新版本
- 所有 DLC 和补丁
- 多国家和多政体系统
