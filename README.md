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
├── SKILL.md              # Skill入口（boss-skill-creator）
├── prompts/             # 生成模板
│   ├── intake.md         # 信息录入
│   ├── decision_analyzer.md  # 决策分析
│   ├── decision_builder.md  # decision.md 模板
│   ├── business_builder.md  # business_context.md 模板
│   ├── persona_builder.md   # persona.md 模板
│   └── skill_builder.md    # SKILL.md 生成模板
├── tools/               # 数据采集工具
│   ├── feishu_parser.py         # 飞书文档解析
│   ├── feishu_auto_collector.py # 飞书自动采集（需开放平台权限）
│   ├── feishu_browser.py        # 飞书浏览器方案（需登录态）
│   └── email_parser.py          # 邮件解析
└── boss/                 # 生成的Boss Skill
    └── {slug}/           # ⚠️ 建议加入 .gitignore 保护隐私
        ├── SKILL.md          # 主入口（第一人称）
        ├── decision.md       # 决策框架+权力结构
        ├── business_context.md  # 业务边界+OKR/KPI
        ├── persona.md        # 人格特质（Layer 0-4）
        ├── meta.json         # 元数据
        └── knowledge/
            └── raw_materials.md  # 原始素材
```

---

## 安装

### Claude Code / OpenClaw

```bash
# 安装到全局
git clone https://github.com/gold3bear/boss-skill ~/.openclaw/workspace/skills/boss-skill

# 或安装到项目
mkdir -p .claude/skills
git clone https://github.com/gold3bear/boss-skill .claude/skills/boss-skill
```

---

## 数据来源

Boss Skill 的知识来源，按优先级排序：

| 优先级 | 来源 | 说明 |
|-------|------|------|
| 🥇1st | 业务架构文档 | 飞书/Notion/Confluence 等 |
| 🥈2nd | OKR/KPI 文档 | 老板的 OKR、团队 KPI |
| 🥉3rd | 聊天记录 | 关键决策案例、表达风格 |
| 4th | 周报/邮件 | 历史决策背景 |

### 导入方式

```
[A] 飞书文档链接 — 直接提供飞书文档 URL
[B] 直接粘贴内容 — 复制文档内容粘贴
[C] 描述补充 — 用文字描述老板的决策风格
```

### 依赖安装（可选）

```bash
# 安装所有依赖
pip3 install -r requirements.txt

# 或单独安装
pip3 install pypinyin        # 中文姓名转拼音 slug
pip3 install playwright      # 飞书浏览器方案
pip3 install python-docx     # Word .docx 转文本
pip3 install openpyxl        # Excel .xlsx 转 CSV
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
/boss {slug}              # 完整Boss Skill（第一人称沉浸式）
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

## .gitignore 配置

建议将生成的 Boss Skill 加入项目 `.gitignore`：

```gitignore
# Boss Skill 生成的隐私内容
boss/bosshuang/
boss/*/meta.json
```

---

## 参考资料

- [Colleague Skill](https://github.com/gold3bear/colleague-skill) — 同事Skill，本项目的参考框架

---

## License

MIT License
