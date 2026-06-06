# 🎨 设计品味引擎 — Design Taste Engine

> **让你的 AI 编程 Agent 拥有专业前端设计师的品味。**  
> 1,200+ 行精编指令，系统性地消除 AI 生成界面中的「廉价模板感」。

---

## 效果对比

| 不用本 Skill | 使用本 Skill |
|-------------|-------------|
| 紫色渐变 + 居中英雄区块 | 根据品牌基调动态选择布局方向 |
| 三张一模一样的功能卡片 | 不对称 Bento 网格 + 交错节奏 |
| Inter + slate-900 默认感 | Geist / Cabinet Grotesk / Satoshi 等有性格的字体 |
| 静态页面 | GSAP / Motion 物理动效 |
| 模板感（一看就是 AI 写的） | 定制感（像人类设计师做的） |

---

## 适用平台

| 平台 | 安装方式 | 状态 |
|------|---------|------|
| **Claude Code** | → `~/.claude/skills/design-taste-frontend/` | ✅ 已验证 |
| **Cursor** | → `~/.cursor/skills-cursor/` | ✅ 已验证 |
| **Pi** | → `~/.pi/agent/skills/` | ✅ 已验证 |
| **Codex** | → 项目 `.claude/skills/` | ✅ 已验证 |

---

## 快速安装

### Claude Code

```bash
# 手动克隆
git clone https://github.com/daijinou/design-taste-skill.git
cp -r design-taste-skill/skill ~/.claude/skills/design-taste-frontend

# 或使用 ccpi（如果已安装）
ccpi install design-taste-frontend
```

### Cursor

```bash
# 复制到 Cursor skills 目录
cp -r design-taste-skill/skill ~/.cursor/skills-cursor/design-taste-frontend
```

### Pi

```bash
# 复制到 Pi skills 目录（或创建软链接）
cp -r design-taste-skill/skill ~/.pi/agent/skills/design-taste-frontend
```

---

## 核心理念

### 三旋钮调控（Three Dials）

每次生成前，先设定三个全局变量：

```
DESIGN_VARIANCE: 8    ← 1(完全对称) → 10(艺术混沌)
MOTION_INTENSITY: 6   ← 1(静态) → 10(电影级物理)
VISUAL_DENSITY: 4     ← 1(美术馆留白) → 10(驾驶舱密集)
```

所有设计决策都基于这三个旋钮的数值，而不是 AI 的默认统计偏好。

### 智能读题（Brief Inference）

AI 不再默认输出「紫色渐变+居中英雄页」。它会先分析：

1. **页面类型** — SaaS / 作品集 / 活动页 / 编辑页面
2. **情绪语言** — 极简 / 奢华 / 工业 / 玩味
3. **受众** — B2B 采购决策者 vs 设计意识强的消费者
4. **品牌资产** — 已存在的 Logo / 颜色 / 字体

### 反模式绝对禁止（Absolute Zero）

- ❌ 紫色/蓝色霓虹渐变
- ❌ 三张等大功能卡
- ❌ Inter 字体
- ❌ 玻璃拟态乱用
- ❌ 居中英雄 + 深色网格背景
- ❌ 暖米色 + 黄铜色 + 深咖啡色（"精品消费品牌"模板）

---

## 包含什么

```
skill/
├── SKILL.md          # 核心指令（1,200+ 行）
├── references/       # 参考资源
│   ├── typography.md # 字体搭配指南
│   └── palette.md    # 色板轮换规则
└── README.md         # 本文件
```

### 技能覆盖

| 模块 | 内容 |
|------|------|
| **§0 读题** | 页面分类、情绪推断、受众分析、约束识别 |
| **§1 三旋钮** | 变量映射、场景预设、交叉引用 |
| **§2 设计系统映射** | Fluent / Material / Carbon / shadcn/ui 等官方系统选择器 |
| **§3 默认架构** | React/Next.js 脚手架、状态管理、图标库、CSS 策略 |
| **§4 设计工程** | 字体选择规则、配色校正、布局多样化、材质与阴影、交互状态 |
| **§5 动效** | ScrollTrigger、图块覆盖、交错入场、横向滚动、磁吸按钮 |
| **§6 响应式规则** | 移动端折叠策略、弹窗/导航溢出处理 |
| **§7 移动端独立规则** | 与桌面端不同的设计考量 |
| **§8-10 审计与交付** | 预飞行检查清单、可访问性、性能 |

---

## 许可证

**个人使用许可证** — 购买后可在个人/团队项目中使用。禁止转售、分发或作为独立产品再包装。

---

## 作者

[daijinou](https://github.com/daijinou) — 前端设计师 / AI Agent 工程实践者

---

## 更新日志

### v1.0.0 (2026-06-06)
- 首次发布
- 完整 1,200+ 行设计品味指令
- 支持 Claude Code / Cursor / Pi / Codex 平台
