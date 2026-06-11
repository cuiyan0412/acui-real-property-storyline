# 安装指南

本 skill 的核心文件 `SKILL.md` 是平台无关的纯 Markdown 方法论文档，理论上任何能读取 Markdown 的 AI Agent 都能使用。但不同 AI 工具的"安装"和"触发"机制不同，本文档给你三种主流工具的具体操作步骤。

---

## 安装难度对比

| 工具 | 安装难度 | 触发方式 | 推荐度 |
|---|---|---|---|
| **QoderWork** | ⭐ 一键安装 | 关键词自动 + `@skill` 主动 | 体验最完整 |
| **Claude Code** | ⭐⭐ 解压放目录 | description 关键词自动 | 流畅 |
| **Codex CLI / 其他** | ⭐⭐⭐ 手动注入 | 用户主动引用 | 可用 |

---

## 方法一：QoderWork（推荐）

**前提**：已安装 [QoderWork](https://docs.qoder.com/qoderwork/introduction) 桌面端。

### 步骤

1. 从 GitHub Releases 页面下载 `acui-real-property-storyline.skill` 文件
2. 打开 QoderWork，把文件**直接拖进对话窗口**
3. 在对话里点击渲染出来的 **"Save skill"** 按钮
4. 安装完成

### 触发方式

任何包含以下关键词的对话都会自动激活：
- 地产故事线 / 项目故事线 / 项目定位 / 项目策划
- 案名策划 / 营销主题 / 招商招租脚本
- 写字楼故事线 / 住宅故事线 / 商业故事线
- 产业园故事线 / 特色街区故事线 / 品牌叙事

也可以主动调用：`@skill 商业` / `@skill 住宅` / `@skill 办公`。

---

## 方法二：Claude Code

**前提**：已安装 Claude Code，版本 ≥ 2025 年 10 月（带 Agent Skills 功能）。命令行确认：

```bash
claude --version
```

### 步骤

```bash
# 1. 下载 .skill 文件后，把 .skill 改成 .zip 解压
mv acui-real-property-storyline.skill acui-real-property-storyline.zip
unzip acui-real-property-storyline.zip

# 2. 选择安装范围

# A. 用户级（所有项目都能用，推荐）
mkdir -p ~/.claude/skills
mv acui-real-property-storyline ~/.claude/skills/

# 或 B. 项目级（仅当前项目可用）
mkdir -p .claude/skills
mv acui-real-property-storyline .claude/skills/

# 3. 重启 Claude Code 会话
```

### 触发方式

跟 QoderWork 一样靠 description 关键词自动匹配。说出包含"地产故事线 / 项目策划 / 案名 / 招商脚本 / 写字楼故事线 / 商业故事线 / 品牌叙事"等关键词的话即可。

---

## 方法三：Codex CLI

**重要**：Codex CLI 截至当前没有原生 Skills 系统，无法像 Claude Code 那样自动识别。但 SKILL.md 是平台无关的纯方法论文本，**用以下三种方式都能使用**。

### 方式 A：按需引用（推荐）

下载并保存 `SKILL.md` 到任意位置（例如 `~/skills/storyline/SKILL.md`），需要时让 Codex 读取它：

```
帮我读取 ~/skills/storyline/SKILL.md，按里面的方法论给我做一个地产项目的故事线
```

最干净，不污染全局指令。

### 方式 B：项目级注入

在具体项目根目录创建 `AGENTS.md`，把 `SKILL.md` 内容贴进去（或者用 `@SKILL.md` 引用）。该项目内的 Codex 会自动遵循这套方法论。**适合长期跑地产项目的场景**。

### 方式 C：全局指令注入（不推荐）

放到 `~/.codex/instructions.md`，所有 Codex 会话都加载。**会污染其他场景**（写代码时也会带上地产语境）。除非你就是地产专职从业者，否则别用。

---

## 方法四：其他 AI 工具（ChatGPT / Gemini / 通义 / 文心等）

直接复制 `SKILL.md` 全文，发给 AI 后说：

```
请按上面的方法论帮我策划一个地产项目故事线。我的项目信息是：[填业态/城市/板块/开发商/体量/形态等]
```

或者把 SKILL.md 上传为附件让 AI 读取。

---

## 卸载方法

### QoderWork

```bash
# 把 skill 移到回收站
mv ~/.qoderwork/skills/acui-real-property-storyline ~/.Trash/
```

### Claude Code

```bash
# 用户级
rm -rf ~/.claude/skills/acui-real-property-storyline

# 项目级
rm -rf .claude/skills/acui-real-property-storyline
```

---

## 升级 / 更新版本

每个版本会在 GitHub Releases 标记 tag。升级时：

1. 下载最新的 `.skill` 文件
2. 删除旧版本（见上面"卸载方法"）
3. 按"安装"步骤重新装一遍

---

## 常见问题

**Q: 触发不了 skill 怎么办？**
A: 检查三件事 — (1) 文件是否在正确目录；(2) 对话用了 description 里覆盖的关键词；(3) AI 工具是否需要重启会话。如果还是不行，主动说"使用 acui-real-property-storyline 这个 skill"明确触发。

**Q: SKILL.md 里有些路径是 `~/.qoderwork/...`，别的工具能用吗？**
A: 经检查，本 skill 内部**没有 hardcode 任何 QoderWork 专属路径**——文档全是流程描述、判断标准、输出格式，是 100% 可移植的。

**Q: 我能修改 SKILL.md 来定制吗？**
A: 可以，license 允许个人/团队修改。但请保留原作者署名（CC BY-NC 4.0 要求）。如果改得很好，欢迎提 PR 回馈到主仓库。
