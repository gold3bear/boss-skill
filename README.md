# 老板.Skill

> *"理解老板的决策逻辑，在复杂的组织政治中更有效地推进业务。"*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 项目介绍

Boss Skill 是一个将老板/上级"蒸馏"成AI Skill的工具，帮助用户：

- 🎯 **预判决策** — 提前知道老板对新方案的反应
- 🔍 **理解潜台词** — 读懂老板没说出口的意思
- 🤝 **有效推进** — 在组织政治中更顺畅地推进业务
- 📈 **向上管理** — 更好地与老板协作

---

## 与Colleague Skill的区别

| 维度 | Colleague Skill | Boss Skill |
|------|----------------|------------|
| **定位** | 帮你干活 | 帮你预判 |
| **核心内容** | 工作能力+性格 | 决策框架+权力结构 |
| **知识来源** | 技术文档+聊天 | 业务架构+OKR+聊天 |
| **使用场景** | 完成具体任务 | 预判反应+向上管理 |
| **目标用户** | 技术/产品人员 | 中高层管理者 |

---

## 核心知识优先级

| 优先级 | 知识类型 | 说明 |
|--------|---------|------|
| 🥇1st | 部门业务架构 | 业务边界、决策链条、资源分布 |
| 🥈2nd | OKR/KPI | 老板的目标、压力来源、决策动机 |
| 🥉3rd | 老板聊天记录 | 决策案例、表达风格、潜台词 |

---

## 文件结构

```
boss-skill/
├── SKILL.md              # Skill入口
├── README.md              # 说明文档
├── prompts/               # Prompt模板
│   ├── intake.md          # 信息录入
│   ├── decision_analyzer.md # 决策分析
│   ├── power_analyzer.md   # 权力结构分析
│   ├── decision_builder.md # 决策框架生成
│   └── power_builder.md    # 权力结构生成
└── boss/                  # 生成的Boss Skill
    └── {slug}/
        ├── SKILL.md
        ├── decision.md
        ├── power.md
        ├── business_arch.md
        ├── okr_kpi.md
        └── meta.json
```

---

## 安装

### Claude Code / OpenClaw

```bash
# 安装到全局
git clone https://github.com/your-repo/boss-skill ~/.openclaw/workspace/skills/boss-skill

# 或安装到项目
mkdir -p .claude/skills
git clone https://github.com/your-repo/boss-skill .claude/skills/boss-skill
```

---

## 使用

### 创建Boss Skill

```
/create-boss
```

按提示输入老板信息即可。

### 调用Boss Skill

```
/boss {slug}              # 完整Boss Skill
/boss {slug}-decision     # 仅决策框架
/boss {slug}-power        # 仅权力结构
```

---

## 使用场景

| 场景 | 使用方式 | 价值 |
|------|---------|------|
| 写周报前 | "帮我看看老板会问什么" | 预判问题，提前准备 |
| 方案审批前 | "老板看到这个方案会怎么反应" | 预判阻力，调整方案 |
| 跨部门协作前 | "老板会支持还是反对" | 评估可行性 |
| 读懂潜台词 | "老板说这个不做是什么意思" | 理解真实意图 |
| 向上管理 | "老板最近在关心什么" | 调整工作重心 |

---

## 设计理念

> **不是让Boss Skill代替老板做决策，而是帮助用户更好地理解老板的决策逻辑和立场。**

### P9+ Boss的特殊性

- 决策不仅基于数据，还基于政治
- 需要理解业务边界和权力结构
- OKR/KPI是决策的核心驱动力
- 组织政治影响决策

---

## 参考资料

- [Colleague Skill](https://github.com/gold3bear/colleague-skill) — 同事Skill，本项目的参考框架

---

## License

MIT License
