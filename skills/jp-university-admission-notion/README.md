# JP University Admission Notion — 日本大学院募集要项自动解读与归档 Skill

> **完全免费、完全公开。** 这是一个供 [Manus AI](https://manus.im) 使用的 Skill，帮助申请日本大学院的同学快速、准确地解读募集要项（招生简章），并将关键信息结构化归档到 Notion。

## 这个 Skill 能做什么？

日本大学院的募集要项通常是一份几十页的日语 PDF，里面包含了出愿资格、语言要求、材料清单、考试安排、时间节点等大量关键信息。手动逐条整理非常耗时，而且容易遗漏。

当你把一份募集要项发给 Manus 后，这个 Skill 会自动完成以下工作：

1. **严谨信息提取** — 按优先级分三层提取所有关键信息：
   - **核心门槛**（出愿资格、语言要求、事前审查）— 不满足就直接没资格
   - **考试与材料**（选考方式、材料清单、研究计划书要求、报名费）— 准备出愿的核心内容
   - **录取信息**（招生名额、学费奖学金、校区位置）— 辅助决策参考
2. **时间线生成** — 自动生成按时间排序的完整申请日程，标注容易遗漏的截止日期
3. **Notion 归档** — 将所有信息结构化写入 Notion 页面，方便对比多所学校、跟踪出愿进度

**核心原则：零捏造。** 所有信息 100% 来自你提供的文件，找不到的内容会明确标注"文件中未提及"，绝不会自行脑补。

## 使用前提

- 你需要有 [Manus](https://manus.im) 的账号
- 需要在 Manus 中连接 Notion MCP（用于归档）

---

## 从下载到使用：完整指南

如果你不熟悉 GitHub，没关系，按照下面的步骤一步一步来就行。

### 方法一：直接用 GitHub 链接导入（最简单）

这是最推荐的方式，不需要下载任何文件。

1. 打开 [Manus](https://manus.im)，登录你的账号
2. 点击左侧菜单中的 **Skills**（技能）标签页
3. 点击右上角的 **+ Add**（添加）按钮
4. 选择 **Import from GitHub**（从 GitHub 导入）
5. 粘贴本仓库的地址：
   ```
   https://github.com/sonnygin/japan-university-exam-guide
   ```
6. Manus 会自动识别仓库中的 Skill 并导入，点击确认即可

### 方法二：下载 ZIP 后上传

如果你更习惯先下载到本地再上传，按以下步骤操作：

**第一步：从 GitHub 下载**

1. 打开本仓库页面：https://github.com/sonnygin/japan-university-exam-guide
2. 点击绿色的 **Code** 按钮
3. 在弹出的菜单中点击 **Download ZIP**
4. 等待下载完成，你会得到一个 `japan-university-exam-guide-main.zip` 文件

**第二步：解压并找到 Skill 文件夹**

下载的 ZIP 解压后，目录结构大致如下：

```
japan-university-exam-guide-main/
├── skills/
│   ├── academic-cold-email/
│   └── jp-university-admission-notion/    <-- 这就是你需要的 Skill 文件夹
│       ├── SKILL.md
│       ├── README.md
│       └── references/
│           └── notion-archiving.md
├── experiences/
├── tips/
├── resources/
└── README.md
```

你需要的是 `skills/jp-university-admission-notion/` 这整个文件夹。

**第三步：上传到 Manus**

1. 打开 [Manus](https://manus.im)，登录你的账号
2. 点击左侧菜单中的 **Skills**（技能）标签页
3. 点击右上角的 **+ Add**（添加）按钮
4. 选择 **Upload a skill**（上传技能）
5. 将 `jp-university-admission-notion` 文件夹整个拖入上传区域（或者将该文件夹压缩成 ZIP 后上传）
6. 上传成功后，你会在 Skills 列表中看到 **jp-university-admission-notion**

### 导入后：开始使用

无论你用哪种方式导入，使用方法都一样：

1. 在 Manus 中新建一个对话
2. 在输入框中输入 **`/`**（斜杠），会弹出你已安装的 Skills 列表
3. 选择 **jp-university-admission-notion**
4. Manus 会回复确认消息，然后你可以：
   - 直接上传募集要项的 **PDF 文件**
   - 粘贴募集要项的 **网页链接**
   - 直接粘贴募集要项的 **文本内容**
5. Manus 会自动提取信息、生成时间线，展示给你确认后归档到 Notion

**使用示例：**
```
帮我解读这份募集要项：[上传 PDF]
```
```
帮我整理这个大学的招生信息：https://www.xxx-university.ac.jp/admission/guidelines.pdf
```

---

## 文件结构说明

| 文件 | 作用 | 谁在读 |
|------|------|--------|
| `SKILL.md` | Skill 的核心指令文件，定义了完整的工作流程 | Manus AI |
| `README.md` | 本说明文件，介绍功能和使用方法 | 你（人类） |
| `references/notion-archiving.md` | Notion 归档的页面模板和 MCP 调用方式 | Manus AI |

## 特色亮点

- **三级优先级提取**：按"核心门槛 → 考试材料 → 录取信息"分层整理，最重要的信息一目了然
- **消印有効 vs 必着 区分**：自动识别并高亮截止日期是"邮戳有效"还是"必须送达"，这个细节经常被忽略但非常致命
- **缺失信息标注**：找不到的信息不会跳过，而是明确标注"文件中未提及，需自行确认"
- **时间线自动生成**：所有日期按时间排序，容易遗漏的截止日期会特别标注
- **出愿状态跟踪**：Notion 归档页面包含出愿状态字段（未开始/准备中/已出愿/已考试/已合格），方便管理多校申请
- **零捏造原则**：所有信息 100% 来自原文件，绝不脑补

## 常见问题

**Q：我没有 Notion 怎么办？**
A：Notion 归档是最后一步，即使没有连接 Notion，前面的信息提取和时间线生成仍然可以正常使用。你可以手动复制整理好的内容保存到其他地方。

**Q：可以一次处理多份募集要项吗？**
A：可以。在一次对话中依次发送多份文件，Manus 会逐一处理。

**Q：募集要项是日语的，能看懂吗？**
A：完全没问题。Skill 专门为日语募集要项设计，提取后的信息会用中文呈现，方便你理解。

**Q：PDF 扫描件能处理吗？**
A：如果 PDF 是文字版（可以复制文字），完全没问题。如果是纯扫描图片版，可能无法提取文字，建议你提供网页链接或手动复制关键文字。

**Q：我不会用 GitHub，也不知道什么是 Skill，能用吗？**
A：完全可以。只要你有 Manus 账号，按照上面「方法一」的 6 个步骤操作就行，全程不需要任何技术背景。

## 贡献与反馈

如果你在使用中发现问题或有改进建议，欢迎提 Issue 或 Pull Request！
