# Academic Cold Email — 日本大学院套瓷信自动生成 Skill

> **完全免费、完全公开。** 这是一个供 [Manus AI](https://manus.im) 使用的 Skill，帮助申请日本大学院修士课程的同学自动化完成从教授调研到套瓷信撰写的全流程。

## 这个 Skill 能做什么？

当你提供一个日本大学教授的主页链接后，它会自动完成以下全部工作：

1. **深度情报收集** — 自动浏览教授主页及所有子页面（研究介绍、论文列表、招生说明等），提取教授的研究方向、近期论文、联系方式、以及是否有特殊联系要求
2. **研究方向拟定** — 结合教授的研究重点和你的个人背景，自动生成一个具体可行的研究方向作为套瓷切入点
3. **中英文套瓷信生成** — 分别生成英文版和中文版的套瓷信，引用教授的具体论文，融入拟定的研究方向和你的优势
4. **Notion 归档** — 将教授信息、研究分析、套瓷信全部归档到 Notion 页面，方便跟踪管理多位教授的套瓷进度

## 使用前提

- 你需要有 [Manus](https://manus.im) 的账号
- 需要在 Manus 中连接 Notion MCP（用于归档套瓷记录）

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
│   └── academic-cold-email/    <-- 这就是你需要的 Skill 文件夹
│       ├── SKILL.md
│       ├── README.md
│       └── references/
│           ├── email-template.md
│           └── notion-archiving.md
├── experiences/
├── tips/
├── resources/
└── README.md
```

你需要的是 `skills/academic-cold-email/` 这整个文件夹。

**第三步：上传到 Manus**

1. 打开 [Manus](https://manus.im)，登录你的账号
2. 点击左侧菜单中的 **Skills**（技能）标签页
3. 点击右上角的 **+ Add**（添加）按钮
4. 选择 **Upload a skill**（上传技能）
5. 将 `academic-cold-email` 文件夹整个拖入上传区域（或者将该文件夹压缩成 ZIP 后上传）
6. 上传成功后，你会在 Skills 列表中看到 **academic-cold-email**

### 导入后：开始使用

无论你用哪种方式导入，使用方法都一样：

1. 在 Manus 中新建一个对话
2. 在输入框中输入 **`/`**（斜杠），会弹出你已安装的 Skills 列表
3. 选择 **academic-cold-email**
4. Manus 会先问你三个基本信息：
   - 你的姓名
   - 当前院校和专业
   - 你的核心技能与经历优势
5. 然后发送你想套瓷的教授主页链接，例如：
   ```
   帮我给这位教授写套瓷信：https://www.xxx-lab.jp/professor/
   ```
6. Manus 会自动执行全流程：调研 → 拟题 → 写信 → 归档到 Notion

---

## 文件结构说明

| 文件 | 作用 | 谁在读 |
|------|------|--------|
| `SKILL.md` | Skill 的核心指令文件，定义了完整的工作流程 | Manus AI |
| `README.md` | 本说明文件，介绍功能和使用方法 | 你（人类） |
| `references/email-template.md` | 中英文套瓷信的写作模板和规范 | Manus AI |
| `references/notion-archiving.md` | Notion 归档的页面模板和 MCP 调用方式 | Manus AI |

## 特色亮点

- **支持日语页面**：能识别日语学术网站的常见导航结构（研究内容、業績、受験生へ 等）
- **红线检查机制**：自动检测教授是否有特殊联系要求或明确表示不招生，避免踩坑
- **中英双语输出**：两封信独立撰写，不是简单互译，各自符合对应语言的学术书信习惯
- **零捏造原则**：所有论文、邮箱、信息均来自实际浏览的页面，不会编造任何内容
- **状态跟踪**：Notion 归档页面包含套瓷状态字段（待发送/已发送/已回复/不招生），方便管理

## 常见问题

**Q：我没有 Notion 怎么办？**
A：Notion 归档是最后一步，即使没有连接 Notion，前面的教授调研和套瓷信生成仍然可以正常使用。你可以手动复制生成的内容保存到其他地方。

**Q：可以一次套瓷多位教授吗？**
A：可以。在一次对话中提供多个教授主页链接，Manus 会依次处理每一位教授。

**Q：生成的套瓷信可以直接发送吗？**
A：建议你在发送前仔细检查一遍内容，确认信息准确、语气合适。AI 生成的内容是一个很好的起点，但最终发送前的把关还是要靠自己。

**Q：我不会用 GitHub，也不知道什么是 Skill，能用吗？**
A：完全可以。只要你有 Manus 账号，按照上面「方法一」的 6 个步骤操作就行，全程不需要任何技术背景。

## 贡献与反馈

如果你在使用中发现问题或有改进建议，欢迎提 Issue 或 Pull Request！
