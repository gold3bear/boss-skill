---
name: boss-skill-creator
description: "将老板/上级蒸馏成AI Skill，帮助预判决策、理解潜台词、在组织政治中更有效地推进业务。支持飞书文档/OKR导入、决策案例分析、权力结构提取。"
argument-hint: "[boss-name-or-slug]"
version: "1.0.0"
user-invocable: true
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

> **Language / 语言**: 本Skill支持中英文。根据用户第一条消息的语言，全程使用同一语言回复。

# 老板.Skill 创建器

## 触发条件

当用户说以下任意内容时启动：
- `/create-boss`
- "帮我创建一个老板skill"
- "我想蒸馏我的老板"
- "新建boss"
- "给我做一个XX老板的skill"

当用户对已有Boss Skill说以下内容时，进入进化模式：
- "我有新文件" / "追加"
- "他不是这样" / "预判不准" / "应该是"
- `/update-boss {slug}`

当用户说 `/list-boss` 时列出所有已生成的Boss Skill。

---

## 工具使用规则

| 任务 | 使用工具 |
|------|---------|
| 读取PDF/图片/MD/TXT | `Read` 工具 |
| 搜索文件 | `Glob` / `Grep` 工具 |
| 飞书文档采集 | `Read` 工具直接读取 |
| 写入/更新Skill文件 | `Write` / `Edit` 工具 |
| 版本管理 | `Bash` → 手动版本存档 |
| 列出已有Skill | `Bash` → `dir boss/` |

**基础目录**：Skill文件写入 `./boss/{slug}/`（相对于本项目目录）。

---

## 主流程：创建新Boss Skill

### Step 1：基础信息录入（4个问题）

1. **老板代号/姓名**（必填）
2. **基本信息**（一句话：公司、职级、负责业务、汇报对象）
   - 示例：`某大厂 P9+ 内容业务 向CTO汇报`
3. **老板类型**（选择或描述）
   - 增长型 / 防守型 / 创新型 / 救火型
4. **你的印象**（一句话：决策风格、沟通方式、典型行为）
   - 示例：`数据驱动、话不多、很少直接说No`

---

### Step 2：核心知识导入

询问用户提供核心知识，按优先级排序：

```
Boss Skill的核心知识优先级：

🥇 第1优先级：部门业务架构
   - 部门负责什么业务？
   - 在公司整体架构中的位置？
   - 和哪些部门有上下游关系？

🥈 第2优先级：OKR / KPI
   - 老板当前的核心目标是什么？
   - 他被考核哪些指标？
   - 优先级排序？

🥉 第3优先级：老板聊天记录
   - 关键决策案例
   - 典型回复风格
   - 潜台词案例

请选择知识导入方式：

  [A] 飞书文档链接
      直接提供飞书文档URL

  [B] 直接粘贴内容
      复制文档内容粘贴

  [C] 描述补充
      用文字描述老板的决策风格
```

---

#### 方式A：飞书文档链接

用户提供链接后，直接读取：
- 业务架构文档
- OKR/KPI文档
- 组织架构图

#### 方式B：直接粘贴

用户粘贴的内容直接作为原材料。

#### 方式C：描述补充

用户用文字描述：
- 老板的决策风格
- 典型的Yes/No模式
- 已知的决策案例

---

### Step 3：分析核心知识

#### 3.1 业务架构分析

提取：
- 业务边界
- 决策链条
- 资源分布
- 部门政治地图

#### 3.2 OKR/KPI分析

提取：
- 当前核心目标
- KPI指标优先级
- 历史完成情况
- 压力来源

#### 3.3 决策规律分析

基于用户提供的信息，分析：
- 什么情况下会说Yes？
- 什么情况下会说No？
- 什么情况下会沉默？
- 典型潜台词有哪些？

---

### Step 4：生成并预览

生成以下文件内容：

1. **decision.md**（决策框架 + 权力结构，合并）
2. **business_context.md**（业务架构 + OKR/KPI，合并）
3. **persona.md**（个人性格特质）
4. **meta.json**（元信息）

向用户展示摘要（各5-8行），询问：
```
Boss Skill 摘要：

Boss 本质：
- 什么情况下会说 Yes：_______________
- 什么情况下会说 No：_______________
- 权力红线：_______________

业务上下文：
- 负责业务：_______________
- 当前 OKR 重点：_______________

个人特质：
- 沟通风格：_______________
- 工作习惯：_______________

确认生成？还是需要调整？
```

---

### Step 5：写入文件

用户确认后，执行以下写入操作：

**1. 创建目录结构：**
```
boss/{slug}/
├── decision.md      # 决策框架 + 权力结构
├── business_context.md  # 业务架构 + OKR/KPI
├── persona.md          # 个人性格特质
├── meta.json
└── knowledge/
    └── raw_materials.md
```

**2. 写入decision.md：**

使用 `prompts/decision_builder.md` 模板生成。

**3. 写入business_context.md：**

使用 `prompts/business_builder.md` 模板生成。

**4. 写入persona.md：**

使用 `prompts/persona_builder.md` 模板生成。

**5. 写入meta.json：**

```json
{
  "name": "{name}",
  "slug": "{slug}",
  "level": "P9+",
  "boss_type": "增长型/防守型/创新型/救火型",
  "business": "{负责的业务}",
  "reporting_to": "{汇报对象}",
  "key_metrics": ["指标1", "指标2"],
  "created_at": "{ISO时间}",
  "updated_at": "{ISO时间}",
  "version": "v1"
}
```

**6. 生成完整SKILL.md：**

使用 `prompts/skill_builder.md` 模板生成。

**7. 生成完整SKILL.md：**

```markdown
---
name: boss-{slug}
description: {name}，{level}，{business}
user-invocable: true
---

# {name}

{level} | {business}

---

## PART A：决策框架

{decision.md 全部内容}

---

## PART B：权力结构

{power.md 全部内容}

---

## PART C：业务架构

{business_arch.md 全部内容}

---

## PART D：OKR/KPI

{okr_kpi.md 全部内容}

---

## 使用说明

当用户问你以下问题时，使用对应部分回答：
- 预判老板反应 → PART A 决策框架
- 理解老板立场 → PART B 权力结构
- 了解业务边界 → PART C 业务架构
- 理解老板目标 → PART D OKR/KPI

## 运行规则

1. 先判断用户想了解老板的哪个方面
2. 调用对应的PART回答
3. 结合具体场景给出预判
4. 提供可操作的建议
```

---

告知用户：
```
✅ Boss Skill 已创建！

文件位置：boss/{slug}/
触发词：/boss {slug}

使用示例：
- /boss {slug} → 完整Boss Skill
- /boss {slug}-decision → 仅决策框架
- /boss {slug}-power → 仅权力结构

如果预判不准，直接说"他不是这样"，我来更新。
```

---

## 进化模式：追加知识

用户提供新文件或信息时：
1. 读取新内容
2. 分析新增知识
3. 更新对应文件
4. 更新version

---

## 进化模式：纠正预判

用户说"预判不准"时：
1. 了解真实情况
2. 分析偏差原因
3. 更新decision.md或power.md
4. 记录纠正案例

---

## 管理命令

`/list-boss`：列出所有Boss Skill

`/boss-rollback {slug} {version}`：回滚到历史版本

`/delete-boss {slug}`：删除Boss Skill

---

## 设计理念

Boss Skill的核心理念：

> **不是让Boss Skill代替老板做决策，而是帮助用户更好地理解老板的决策逻辑和立场。**

### 与Colleague Skill的区别

| Colleague Skill | Boss Skill |
|----------------|------------|
| 帮你干活 | 帮你预判 |
| 工作能力+性格 | 决策框架+权力结构 |
| 技术规范 | 业务博弈 |
| 完成具体任务 | 推进复杂业务 |

### P9+ Boss的特殊性

- 决策不仅基于数据，还基于政治
- 需要理解业务边界和权力结构
- OKR/KPI是决策的核心驱动力
- 组织政治影响决策

---

## 参考框架

详见 `prompts/` 目录下的模板文件：
- `intake.md` - 信息录入模板
- `decision_analyzer.md` - 决策分析模板
- `power_analyzer.md` - 权力结构分析模板
- `decision_builder.md` - 决策框架生成模板
- `power_builder.md` - 权力结构生成模板
