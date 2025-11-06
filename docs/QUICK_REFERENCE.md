##############################
# 作弊菜单 - 快速参考指南
##############################

## API 查询总结

### 服务器信息
- **名称**: EU5 Modifier MCP Server
- **版本**: 2.0.0
- **总数据条**: 29,122

### 数据类型分布
| 类型         | 数量   | 用途                                   |
| ------------ | ------ | -------------------------------------- |
| data_type    | 24,442 | 基本数据类型和函数                     |
| effect       | 1,324  | 游戏效果（如 add_gold, set_stability） |
| modifier     | 1,855  | 修改器定义                             |
| trigger      | 1,500  | 条件判断                               |
| event_target | 1      | 事件目标                               |

### 关键效果列表

#### 经济效果
```
add_gold             # 增加黄金
add_manpower         # 增加人力
add_sailors          # 增加水手
```

#### 稳定性效果
```
set_stability        # 设置稳定性（0-3）
add_stability        # 增加稳定性
set_legitimacy       # 设置正统性（0-3）
add_legitimacy       # 增加正统性
add_prestige         # 增加威望
```

#### 军事效果
```
set_professionalism  # 设置专业性（0-1）
add_army_tradition   # 增加陆军传统
add_navy_tradition   # 增加海军传统
```

#### 政府效果
```
add_republican_tradition    # 增加共和传统
add_devotion               # 增加忠诚度
add_horde_unity            # 增加部落统一性
add_reform_progress        # 增加改革进度
set_absolutism             # 设置专制权力（0-3）
```

#### 宗教效果
```
add_karma                  # 增加业力
add_harmony                # 增加和谐度
add_doom                   # 增加末日
```

#### 研究效果
```
add_research_progress      # 增加研究进度
```

#### 地图效果
```
discover_all_provinces     # 发现所有省份
lift_fog_of_war            # 解除战争迷雾
```

#### 其他效果
```
add_war_exhaustion         # 改变战争疲惫（+增加/-减少）
add_corruption             # 改变腐败（+增加/-减少）
add_mercantilism           # 增加重商主义
add_inflation              # 改变通货膨胀（+增加/-减少）
```

### 支持的作用域

所有实现的 ScriptedGui 都支持以下作用域：
- **country**: 国家作用域（主要）
- **international_organization**: 国际组织作用域

### 修改器系统

#### 可用修改器类别
- Location (地点)
- Country (国家)
- Character (角色)
- Unit (单位)

#### 常用修改器属性
```
build_cost              # 建造成本修改
recruitment_cost        # 招募成本修改
build_time              # 建造时间修改
recruitment_time        # 招募时间修改
morale_damage           # 伤害修改
unit_morale             # 士气修改
unrest                  # 全国动乱修改
local_unrest            # 本地动乱修改
```

### 实现模式

#### 模式 1: 直接效果
```
scripted_gui = {
    name = "button_name"
    context_type = country
    on_select = {
        add_gold = 10000
    }
}
```

#### 模式 2: 变量切换
```
scripted_gui = {
    name = "toggle_button_name"
    context_type = country
    on_select = {
        if = {
            limit = { has_variable = toggle_var }
            remove_variable = toggle_var
        }
        else = {
            set_variable = toggle_var
        }
    }
}
```

#### 模式 3: 修改器应用
```
scripted_modifier = {
    name = modifier_name
    icon = "path/to/icon.dds"
    build_cost = -0.5
    recruitment_cost = -0.5
}
```

### 值范围参考

| 属性            | 最小值 | 最大值 | 用途            |
| --------------- | ------ | ------ | --------------- |
| stability       | 0      | 3      | 国家稳定性      |
| legitimacy      | 0      | 3      | 正统性（专制制) |
| prestige        | -      | -      | 威望（无上限）  |
| professionalism | 0      | 1      | 军队专业性      |
| absolutism      | 0      | 3      | 专制权力        |
| war_exhaustion  | -      | 20     | 战争疲惫        |

### 检查列表

- ✓ 所有 35 个按钮已实现
- ✓ 所有 4 个修改器已定义
- ✓ 所有 7 个触发条件已创建
- ✓ 月度效果处理已实现
- ✓ 文件组织完成
- ✓ API 兼容性验证

### 文件位置

```
cheat_menu/
├── in_game/
│   ├── common/
│   │   ├── scripted_guis/
│   │   │   └── cheat_menu_scripted_guis.txt
│   │   ├── scripted_effects/
│   │   │   └── cheat_menu_modifiers_effects.txt
│   │   └── IMPLEMENTATION_SUMMARY.md
│   ├── gui/
│   │   └── cheat_menu_window.gui (原始文件)
│   └── localization/
│       ├── english/
│       │   └── cheat_menu_l_english.yml
│       └── simp_chinese/
│           └── cheat_menu_l_simp_chinese.yml
```

### 调试提示

1. **按钮不响应**: 检查 GUI 中的 onclick 是否正确引用 ScriptedGui 名称
2. **效果无效**: 验证作用域是否正确（country 作用域）
3. **修改器不显示**: 检查 has_modifier 条件是否满足
4. **性能问题**: 考虑减少月度效果的频率

### 相关命令

控制台命令参考（如果启用作弊模式）：
```
add_gold <amount>
add_manpower <amount>
add_sailors <amount>
set_stability <value>
set_legitimacy <value>
add_prestige <amount>
discover_all_provinces
lift_fog_of_war
```

### 进一步开发建议

1. 添加参数化界面（允许用户输入金额）
2. 实现条件显示（仅显示适用的按钮）
3. 添加撤销功能
4. 创建预设配置文件
5. 国际化本地化支持
