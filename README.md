# email-html-template

面向 **营销 / 事务类 HTML 邮件** 的 Agent Skill：用 **结构化 JSON** 做文案与结构契约，再生成兼容 **Gmail、阿里云直邮、Outlook（弱一致预期）** 的表格版 HTML，并带 **模版结构校验、内容审核、模版审核** 三道闸门（支持并行独立 Agent 审核）。

- **Skill 载体**：名为 **`email-html-template`** 的文件夹，内含 **`SKILL.md`**（与 frontmatter 里 `name: email-html-template` 一致）。在本仓库中该目录当前位于 **`.cursor/skills/email-html-template/`**。
- **版本**：见 `SKILL.md` 顶部 `version` 字段

## 这个 Skill 做什么

1. **澄清**发送场景、占位符格式（如 `{{name}}`）、语言与邮件类型。  
2. **只输出 JSON**（subject / preheader / sections…），禁止模型直接吐整页 HTML。  
3. 由 JSON **渲染**内联样式为主的 `table` 邮件 HTML。  
4. **结构校验**（安全、链接、退订位、纯文本、Outlook 嵌套等）。  
5. **内容审核**（文案、合规、语气）。  
6. **模版审核**（与 JSON 一致、客户端风险、垃圾邮件启发式）。  
7. 汇总交付 JSON + HTML + 纯文本 + 审核摘要。

版式与审美准则写在 Skill 正文内，**不依赖**其他 design skill。

## 怎么「让 AI 装上」

**省事做法**：在任意支持 Agent 的对话里说明仓库地址，让 AI 代为安装即可，例如：

> **请克隆 `git@github.com:zhourong12/email-html-template.git`，安装一下这个skills**

由 AI 根据你当前环境（Cursor、OpenCode、Claude Code 等）选择正确目录并完成放置；装好后按各产品方式 **启用该 skill**，或在对话中说「按 email-html-template / 邮件 HTML skill 执行」。

---

Skill 不是可执行安装包，本质仍是：**含 `SKILL.md` 的目录**放进宿主约定的 skills 路径，并在对话里引用。下面是各平台常见位置（**以各工具最新文档为准**）。

### Cursor

1. 将本仓库中的目录 **`email-html-template`**（内含 `SKILL.md`）放到项目的 **`.cursor/skills/`** 下：  
   `项目根/.cursor/skills/email-html-template/SKILL.md`
2. 在 Cursor 里为 Agent **启用该 Skill**（或对话中说明「按 email-html-template 执行」）。
3. 触发示例：邮件模板、`/email-html`、Gmail 邮件兼容、阿里云直邮 等（见 Skill 文末触发词）。

**个人全局**：也可复制到用户目录下的 Cursor skills（以你本机 Cursor 文档为准，常见为 `~/.cursor/skills/`）。

### OpenCode

1. 将 **`email-html-template/SKILL.md`** 放到 OpenCode 会扫描的路径之一，例如：  
   - 项目：`.opencode/skills/email-html-template/SKILL.md`  
   - 或全局：`~/.config/opencode/skills/`（以 [OpenCode Skills 文档](https://opencode.ai/docs/skills) 为准）
2. 目录名须与 frontmatter 里 **`name: email-html-template`** 一致。
3. `metadata` 已使用扁平键值（如 `requires-bins: none`），便于各宿主解析。

### Claude Code / 其他「SKILL.md」生态

将 **`email-html-template` 文件夹**（内含 `SKILL.md`）放入该工具文档指定的 skills 目录（常见为 **`~/.claude/skills/`** 或项目内 `.claude/skills/`），再在对话中引用该 skill。

### GitHub CLI `gh skill`（若已安装新版 gh）

若使用 **`gh skill install`** 从本仓库安装，以 **GitHub CLI 官方手册** 为准，命令与目录约定随版本变化。

## 适用平台（宿主）

| 宿主 | 说明 |
|------|------|
| **Cursor** | 常见为项目或用户下的 skills 目录（见 Cursor 文档） |
| **OpenCode** | 如 `.opencode/skills/` 等（见 [OpenCode Skills](https://opencode.ai/docs/skills)） |
| **Claude Code** | 常见为 `.claude/skills/` 或全局等价路径（见官方文档） |
| **其他支持 Markdown Skill + frontmatter 的 Agent** | 复制 `email-html-template` 目录；**`name` 与文件夹名一致** |

邮件 **收件端** 目标：**Gmail Web/应用、阿里云直邮发出的 HTML、Outlook（版式弱一致）**；Skill 正文不绑定某一发信 SaaS。

## 仓库与同步

```bash
git clone git@github.com:zhourong12/email-html-template.git
```

克隆后，从仓库中取出 **`email-html-template`** 目录（本仓库内路径为 `.cursor/skills/email-html-template/`），再按你所用 AI 工具的 skills 规范放置。HTTPS 克隆：`https://github.com/zhourong12/email-html-template.git`。

## 许可

若未单独提供 `LICENSE`，默认以仓库内文件为准；Skill 内容为使用说明，按需在团队内共享即可。
