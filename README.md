# 旷野像素修仙 · Kaungye Pixel Xiuxian

单文件 HTML5 Canvas 像素风修仙横版动作游戏（Demo）。全部画面由 Canvas 2D 的 `fillRect` 与 Emoji 绘制，无框架、无构建、无外部图片素材。

## 运行方式

双击 `index.html` 用浏览器打开即可，或用任意静态服务器托管：

```bash
python -m http.server 8080
# 打开 http://localhost:8080/index.html
```

## 操作

| 按键 | 动作 | 消耗 / 冷却 |
|---|---|---|
| A / D 或方向键 | 左右移动 | — |
| Space | 跳跃（可二段跳） | 二段跳耗罡气 15 |
| Ctrl | 疾跑 | 体力 36/s |
| Shift | 罡冲（闪避，带无敌帧） | 罡气 25，CD 0.5s |
| 鼠标左键 | 普攻 | CD 0.7s |
| E | 法术「青风诀」 | 灵力 20，CD 3s，命中得风系附魔 4s / 3 充能 |
| Q | 神通「罡风领域」 | 短按开 / 停域，长按 0.45s 释放终结爆发 |
| U | 帮助面板 | — |

## 核心系统

- 角色「流浪者」，称号「初入修行的散修」，武器为拳头。
- 五条资源：气血、体力、罡气、灵力、心神，各上限 100。灵力与心神只在站立时回复。
- 地图宽度 `MAP_W = 32000`，村庄位于 x ≈ 4500–29000。
- 村庄当前包含 26 户民居与 29 处特殊建筑（土地庙、粮仓 ×2、磨坊、猪圈、鸡圈、鸭圈、鹅圈、马圈、茶棚、学堂、医馆、柴房 ×2、神树广场、祠堂、戏台、铁匠棚、酒坊、大集市、木匠铺、晒谷场、豆腐坊、水井 ×4 等）。

## 锁定数值常量

这些常量已多轮确认，改动前必须确认：

| 常量 | 值 |
|---|---|
| SKILL_CD_MAX / ATTACK_CD_MAX / DASH_CD_MAX | 3 / 0.7 / 0.5 |
| DASH_TIME / DASH_QI_COST / JUMP_QI_COST | 0.22 / 25 / 15 |
| QI_REGEN_IDLE / QI_REGEN_MOVE | 7 / 3.5 |
| SPIRIT_REGEN / MIND_REGEN | 2 / 1 |
| STAMINA_REGEN_IDLE / STAMINA_REGEN_WALK / SPRINT_DRAIN | 18 / 10 / 36 |
| SPELL_SPIRIT_COST / DOMAIN_SPIRIT_DRAIN / DOMAIN_MIND_DRAIN | 20 / 8 / 10 |
| MIND_DEBT_TIME / CORRODE_MIND_DRAIN | 3 / 10 |
| BURST_TIME / ULT_HOLD | 0.7 / 0.45 |
| RUN_SPEED / SPRINT_SPEED | 145 / 245 |

## 目录

```
index.html                      游戏全部代码（HTML + CSS + JS）
AGENTS.md                       给 AI 编码助手的接手说明（必读）
docs/requirements-checklist.md   需求核对表与验收标准
```

## 约束

- 纯 2D 正视像素风，禁止伪 3D / 透视。
- 建筑必须贴地、不重叠、门窗不撞墙；烟囱必须贴屋顶坡面。
- 只有民居有烟囱；粮仓无窗无烟囱。
- 篝火永不熄灭，带碰撞与烧伤机制。
