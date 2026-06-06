# 上架指南 — 把你的技能发布到社区

> 以下平台可以直接提交你的 skill。

---

## 1. tonsofskills.com（推荐首选）

**平台规模**: 3,000+ skills，最大聚合器  
**提交方式**: GitHub PR

### 步骤
```bash
# 1. Fork 他们的仓库
# https://github.com/jeremylongshore/claude-code-plugins-plus-skills

# 2. 在 skills/ 下创建你的 skill 目录
# skills/05-frontend-dev/design-taste-engine/

# 3. 复制 skill/SKILL.md 到该目录

# 4. 提交 PR
```

**格式要求**：SKILL.md 需要带标准 frontmatter（已处理好）

---

## 2. tech-leads-club/agent-skills

**平台规模**: 4,500+ stars，14 个分类  
**提交方式**: GitHub PR

### 步骤
```bash
# 1. Fork 他们的仓库
# https://github.com/tech-leads-club/agent-skills

# 2. 在 packages/skills-catalog/skills/ 下创建
# (design)/design-taste-engine/SKILL.md

# 3. 提交 PR
```

**注意**: 他们要求通过安全扫描（已在 frontmatter 中声明 allowed-tools）

---

## 3. buildwithclaude

**平台规模**: 3,000+ stars  
**提交方式**: GitHub PR

### 步骤
```bash
# 1. Fork https://github.com/davepoon/buildwithclaude

# 2. 在 plugins/ 下创建 design-taste-engine/
# 包含 SKILL.md

# 3. 提交 PR
```

---

## 4. GitHub 自家仓库（你也可以自己发）

```bash
# 创建你的发布仓库
git init
git add .
git commit -m "feat: design taste engine v1.0.0"
git tag v1.0.0
git push origin main --tags
```

然后在 GitHub Releases 发布版本。在 README 和社交媒体上推广。

---

## 推广清单

- [ ] 提交到 tonsofskills.com
- [ ] 提交到 tech-leads-club/agent-skills
- [ ] 提交到 buildwithclaude
- [ ] 自己 GitHub 仓库发布
- [ ] 发 Twitter/X（带 demo 截图）
- [ ] 发掘金/知乎文章
- [ ] 发朋友圈（技术圈朋友）
- [ ] 在 Claude/Cursor Discord 里发帖
