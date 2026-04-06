# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Boss.Skill is a prompt-based system that "distills" a boss/manager into an AI Skill. It helps users predict decisions, understand subtext, and navigate organizational politics. This is not a traditional application codebase—it's a Skill template system.

**Design Philosophy**: Two types of Skills coexist:
1. **boss-skill-creator** — The tool/creator (third-person, template-driven)
2. **{slug}/** — The simulated Boss (first-person, immersive roleplay)

## Project Structure

```
boss-skill/
├── SKILL.md              # Main skill entry point (the orchestrator)
├── prompts/               # Generation templates
│   ├── intake.md          # Information collection
│   ├── decision_analyzer.md   # Decision pattern analysis
│   ├── power_analyzer.md      # Power structure analysis
│   ├── decision_builder.md    # decision.md template
│   ├── business_builder.md    # business_context.md template
│   ├── persona_builder.md     # persona.md template (Layered 0-5)
│   └── skill_builder.md       # SKILL.md entry template
└── boss/                  # Generated Boss Skills
    └── {slug}/
        ├── SKILL.md       # Entry point (first-person, references files)
        ├── decision.md    # Decision + Power (merged)
        ├── business_context.md # Business + OKR/KPI (merged)
        ├── persona.md     # Personality (Layered 0-5 structure)
        ├── meta.json      # Metadata
        └── knowledge/
            └── raw_materials.md
```

## Key Concepts

**Two Skill Types**:

| Type | Role | Example |
|------|------|---------|
| creator | Tool/creator | `boss-skill-creator` |
| simulated | Boss persona | `example_xiongshu` |

**decision.md** = Decision Framework + Power Structure (merged)

**business_context.md** = Business Architecture + OKR/KPI (merged)

**persona.md** = MBTI + Communication Style + Work Habits (Layered 0-5)

## Commands

There are no build/test commands—this is a prompt template system. Key operations:

```bash
# List available Boss Skills
ls boss/

# Trigger Boss Skill creation (via /create-boss in Claude Code)
```

## Working with Boss Skills

**Creating a new Boss Skill**:
1. User triggers `/create-boss`
2. Answer questions: name, level, business, MBTI, impression
3. Import knowledge (Feishu docs, paste content, or describe)
4. System generates files using prompts/* templates

**Using an existing Boss Skill**:
- `/boss {slug}` - Full immersive Boss simulation

**Evolution mode**:
- "有新文件" / "追加" - Add new knowledge
- "他不是这样" / "预判不准" - Record correction in persona.md's Correction section

## Persona.md Layered Structure (借鉴自 colleague-skill)

Based on colleague-skill's proven structure:

| Layer | Content | Priority |
|-------|---------|----------|
| Layer 0 | Core personality / Red lines | **Highest** |
| Layer 1 | Identity + MBTI | High |
| Layer 2 | Communication style + dialogue examples | Medium |
| Layer 3 | Decision patterns (Yes/No/Silence) | Medium |
| Layer 4 | Network + politics | Lower |
| Layer 5 | Boundaries + pet peeves | Low |

**Key principle**: Layer 0 overrides everything. Every rule must be concrete behavior, not adjectives.

## Important Patterns

1. **Layer 0 quality determines persona quality**:

   ❌ Bad: "他很强势"
   ✅ Good: "被人质疑方案时，他会反问'你的判断依据是什么'，而不是解释"

2. **First-person immersive**: Generated Skills speak as if they ARE the Boss

3. **MBTI integration**: Extract from chat logs using:
   - Reply speed → E/I
   - Message length → S/N
   - Question style → T/F
   - Planning → J/P

4. **Dialogue examples**: Write as if the Boss is actually talking, not describing

## Reference: colleague-skill

This project was influenced by `colleague-skill` (D:\projects\colleague-skill).

Key borrowings:
- Layered persona structure (0-5)
- Concrete behavioral rules in Layer 0
- "How would you say it" dialogue examples
- Correction record mechanism

Not borrowed (different purpose):
- Work skills (Boss Skills focus on prediction, not tasks)
- Automated chat collection (Boss Skills rely on subjective observation)
