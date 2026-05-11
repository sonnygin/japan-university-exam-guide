# Cold-Email-Check — 日本大学院套瓷信生成 + 强制事实核查 Skill

> **完全免费、完全公开。** 这是一个供 Claude Code 使用的 Skill，在原有的套瓷信自动生成功能之上，新增了**强制性全覆盖事实核查**——自动对套瓷信中的每一项声明进行 40+ 项核查，确保发送前没有任何事实性错误。

## 这个 Skill 和 academic-cold-email 有什么区别？

`academic-cold-email` 负责**生成**套瓷信，`cold-email-check` 负责**生成 + 核查**：

| | academic-cold-email | cold-email-check |
|---|---|---|
| 教授主页深度调研 | ✅ | ✅ |
| 动态生成研究课题 | ✅ | ✅ |
| 中英双语套瓷信 | ✅ | ✅ |
| **自动事实核查** | ❌ | ✅ **42 项全覆盖** |
| **论文内容逐句验证** | ❌ | ✅ 摘要/方法名/数字结论 |
| **技术名词溯源** | ❌ | ✅ 每个名词查一手来源 |
| **招生风险检测** | ❌ | ✅ ○ 标记 + 签证流程图 |
| **偏差即时修正** | ❌ | ✅ 查出来直接改邮件 |
| **核查报告 + 超链接** | ❌ | ✅ 每项附一手来源 |

简单说：`cold-email-check` 先用 `academic-cold-email` 生成草稿，然后**自动（不问你）** 进行三轮全覆盖核查，把所有事实性问题在发送前揪出来。

## 这个 Skill 能做什么？

当你提供一个日本大学教授的主页链接后，它分两个阶段自动完成：

**Phase 1：生成套瓷信草稿**
1. **深度情报收集** — 自动浏览教授主页及所有子页面（研究介绍、论文列表、招生说明等），提取教授的研究方向、近期论文、联系方式、以及是否有特殊联系要求
2. **研究方向拟定** — 结合教授的研究重点和你的个人背景，自动生成一个具体可行的研究方向作为套瓷切入点
3. **中英文套瓷信生成** — 分别生成英文版和中文版的套瓷信，引用教授的具体论文，融入拟定的研究方向和你的优势
4. **Notion 归档** — 将教授信息、研究分析、套瓷信全部归档到 Notion 页面

**Phase 2：自动全面事实核查（无需批准，自动执行）**
- **第一轮（12 项）**：教授身份 — 姓名、职称、所属机构、邮箱、地址、学历、社会任职
- **第二轮（14 项）**：论文内容准确性 — 标题逐字核对、作者顺序验证、摘要内容是否与邮件描述匹配、方法名是否精确、数字结论是否准确
- **第三轮（8 项）**：技术工具与基础设施 — 工具是否存在、功能描述是否正确、版本/协议、架构图
- **第四轮（8 项）**：入学可行性与风险 — 考试日程、签证/COE、招生 ○ 标记、替代申请途径、研究计划可行性

## 使用前提

- 需要安装 [Claude Code](https://claude.ai/code) 的 CLI 或桌面版
- 需要配置**浏览器 CDP**（Chrome 远程调试模式，用于教授页面深度遍历）
- Notion MCP 为可选项（不配置也能正常使用，只是跳过了归档步骤）

## 从下载到使用：完整指南

### 方法一：直接用 GitHub 链接导入（最简单）

1. 打开终端，输入 `claude` 进入 Claude Code
2. 输入 `/plugin marketplace install sonnygin/japan-university-exam-guide`
3. 或者直接输入 `/skill`，选择从 GitHub 导入，粘贴本仓库地址

### 方法二：下载 ZIP 后上传

**第一步：从 GitHub 下载**

1. 打开本仓库页面：https://github.com/sonnygin/japan-university-exam-guide
2. 点击绿色的 **Code** 按钮
3. 在弹出的菜单中点击 **Download ZIP**
4. 等待下载完成，你会得到一个 `japan-university-exam-guide-main.zip` 文件

**第二步：解压并找到 Skill 文件夹**

下载的 ZIP 解压后，目录结构如下：

```
japan-university-exam-guide-main/
├── skills/
│   ├── academic-cold-email/     <-- 基础套瓷信 Skill（cold-email-check 的依赖）
│   ├── cold-email-check/        <-- 带事实核查的套瓷信 Skill
│   │   ├── SKILL.md
│   │   └── README.md
│   └── ...
└── README.md
```

你需要的是 `skills/academic-cold-email/` 和 `skills/cold-email-check/` 这两个文件夹。

**第三步：安装到 Claude Code**

```bash
cp -r academic-cold-email ~/.claude/skills/
cp -r cold-email-check ~/.claude/skills/
```

重启 Claude Code 后即可使用。

### 导入后：开始使用

1. 在终端中输入 `claude` 进入 Claude Code
2. 在输入框中输入 `/`，选择 **cold-email-check**
3. 提供申请者信息（姓名、学历、技能优势）和教授主页链接
4. Claude Code 会自动完成调研 → 拟题 → 写信 → 自动核查全流程
5. 核查报告会直接追加到生成的 md 文件中，每个核查项都附带一手来源超链接

## 文件结构说明

| 文件 | 作用 | 谁在读 |
|------|------|--------|
| `SKILL.md` | Skill 的核心指令文件，定义了生成 + 核查的完整工作流程 | Claude AI |
| `README.md` | 本说明文件，介绍功能和使用方法 | 你（人类） |

注意：`cold-email-check` 依赖 `academic-cold-email` 的模板文件（`references/email-template.md` 和 `references/notion-archiving.md`），所以两个 skill 都必须安装。

## 特色亮点

- **强制性自动核查**：不像其他工具需要你手动要求核查，这个 Skill 在生成草稿后**自动**执行，不需要用户额外确认
- **论文内容级核验**：不只是检查论文标题和日期，还会逐句对比论文摘要与邮件描述是否一致，验证方法名是否精确出现在论文中
- **技术名词溯源**：邮件中出现的每一个技术名词（框架名、方法名、工具名）都会被追溯到一手来源（官方文档/GitHub/论文原文）
- **招生风险检测**：自动检查教授在入试募集表中的 ○ 标记状态，发现不招生时给出替代申请途径建议
- **源链接透明**：所有核查结果附一手来源超链接，你可以逐项审核
- **即时修正**：发现偏差时直接在邮件原文中修改，同时记录在核查报告中，保证一致性

## 常见问题

**Q：我不想被核查，只想快速生成套瓷信怎么办？**
A：那就用 `academic-cold-email`，它是纯生成 Skill，不做核查。`cold-email-check` 适合你想要最高可信度、准备正式发送的场合。

**Q：核查大概需要多久？**
A：取决于教授的网页复杂度，通常在 2-5 分钟。核查会打开多个浏览器标签页、访问 PubMed/DOI/GitHub 等多个一手来源。

**Q：核查报告可以分享给别人吗？**
A：可以。核查报告以 Markdown 表格形式写在你保存的 `.md` 文件中，附带所有来源超链接，可以直接分享。

**Q：这个 Skill 和 academic-cold-email 的依赖关系是怎样的？**
A：`cold-email-check` 在 Phase 1 阶段使用了 `academic-cold-email` 的工作流定义（调研 → 拟题 → 写信），并在 Phase 2 新增了自动核查。两个 Skill 分开管理，各自独立更新。

## 贡献与反馈

如果你在使用中发现问题或有改进建议，欢迎提 Issue 或 Pull Request！
