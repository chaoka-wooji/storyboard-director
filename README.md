# 🎬 Storyboard Director

> 将故事概要点石成金 —— 从一句话梗概到 AI 可执行的全套分镜脚本，六层金字塔式拆解，覆盖从故事到成片的完整管线。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.4-blue.svg)](SKILL.md)
[![Platform](https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Cursor%20%7C%20Codex%20%7C%20Qoder-8A2BE2.svg)]()

---

## 📖 Table of Contents

- [The Problem](#-the-problem)
- [What It Does](#-what-it-does)
- [Quick Example](#-quick-example)
- [How It Works](#-how-it-works)
- [What Makes It Different](#-what-makes-it-different)
- [Installation](#-installation)
- [Use Cases](#-use-cases)
- [Skill Architecture](#-skill-architecture)
- [Example: Tennis Girl](#-example-tennis-girl)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 The Problem

AI 视频生成工具越来越强大，但 **从故事到成片之间有一条巨大的鸿沟**：

- 你有一个好故事，但不知道怎么拆成镜头
- 生成了 6 个独立片段，拼在一起却像 6 个不同的人拍的——没有统一的视觉风格、光线、色调
- 文生图 Prompt 写得太抽象，AI 生成的结果不理想
- 图生视频时不知道怎么描述运动、表情变化、音频对齐点

**Storyboard Director 解决的就是这个问题**——它不只是给你一个 Prompt，而是给你一套完整的影视前期策划方案。

---

## ✨ What It Does

给一个故事概要 + 风格描述 + 目标时长，输出六层专业拆解：

| 模块 | 角色 | 输出 |
|:---:|------|------|
| 一 | 策划总监 | 起/承/转/合宏观时间轴，每段配旁白文案 |
| 二 | 执行导演 | 中观场面序列（地点 + 核心动作），3~10 个场面 |
| 三 | 摄影指导 | 微观蒙太奇分镜——每个场面 3~8 个镜头，含景别/运镜/画面内容/声音设计/时长 |
| 四 | 美术指导 | 视觉设定资料库——角色卡/场景卡/道具卡，精确到颜色/材质/尺寸 |
| 五 | Prompt 设计师 | 每个镜头的文生图 Prompt（英文 + 中文 + 负向提示词 + 设定引用） |
| 六 | 技术指导 | 每个镜头的图生视频动作序列（运动描述/表情时间线/运镜指令/音频对齐点） |

**内置知识底座：**
- 🎥 **镜头语法参考**：景别/角度/运镜/焦点四类体系 + 情绪→镜头映射速查表（10 种情绪）
- 🎨 **视觉风格预设库**：23 种预设风格（电影写实/动画/绘画/风格化），自动匹配或回退用户描述

---

## ⚡ Quick Example

**输入：**
> 故事：13岁女孩小林每天清晨独自练网球，从失败到坚持，偶遇退休教练指导，最终赢得比赛。
> 风格：温情励志 | 时长：3分钟

**输出预览（模块三 —— 微观分镜节选）：**

| 镜号 | 景别 | 运镜 | 画面内容 | 声音设计 | 时长 |
|:---:|------|------|---------|---------|:---:|
| 1 | WS 远景 | 固定 | 蓝灰晨雾中，小林背着大号网球包从右侧走入空旷小路。路灯亮着暖白光晕。 | 远处鸟鸣、晨风、极轻钢琴单音 | 5s |
| 21 | ECU 大特写 | 固定 | 右膝新鲜擦伤约3cm×2cm，粉红真皮浅层露出，透明组织液渗出，沙粒嵌在边缘。 | 完全静默→颤抖呼气→弦乐颤弓 | 2s |
| 42 | WS 远景 | 固定 | 小林保持随挥姿势，球在远角白线弹起白粉。围网外老人竖起大拇指穿过网格。 | 清脆甜区击球声、鸟鸣、温暖大三和弦 | 4s |
| 52 | FS 全景 | 慢动作 Dolly In | 决胜分发球——跳跃最高点→转肩→挥拍→击球瞬间恢复常速，球压缩变形3mm。天窗光束照亮漂浮尘埃。 | 拉长心跳声→清脆击球→体育馆混响 | 5s |

> 完整输出：58 个镜头 × 6 模块，详见 [examples/tennis-girl/](examples/tennis-girl/)

---

## 🏗 How It Works

```
用户输入（故事 + 风格 + 时长）
         │
         ▼
   ┌─────────────────┐
   │  SKILL.md        │  ← 工作流总纲，按需加载子模块
   │  选择生成模式    │     Mode A: 一键全量 / Mode B: 逐模块确认
   └───────┬─────────┘
           │
   ┌───────┼───────────────────────────┐
   ▼       ▼           ▼               ▼
┌──────┐ ┌──────┐ ┌──────────┐ ┌──────────────┐
│模块一 │→│模块二 │→│ 模块三    │→│   模块四      │
│宏观   │ │中观   │ │ 微观分镜  │ │ 视觉设定资料库 │
│时间轴 │ │场面   │ │          │ │              │
│       │ │序列   │ │ ↑参考:    │ │ ↑匹配:        │
│       │ │       │ │ 镜头语法  │ │ 风格预设库    │
└──────┘ └──────┘ └────┬─────┘ └──────┬───────┘
                       │              │
                       ▼              ▼ (单一真相源)
                  ┌──────────┐ ┌──────────────┐
                  │  模块五   │ │   模块六      │
                  │ 文生图    │→│ 图生视频      │
                  │ Prompt    │ │ 动作序列      │
                  └──────────┘ └──────────────┘
```

**级联依赖链**：每个下游模块引用上游模块的输出，确保全片一致性。视觉设定（模块四）是模块五和六的「单一真相源」——所有 Prompt 的角色/场景/道具外观描述必须引用模块四。

---

## 🆚 What Makes It Different

| 维度 | 普通 Prompt 工具 | AI Video Storyboard Skill | **Storyboard Director** |
|------|:---:|:---:|:---:|
| 输出粒度 | 单个 Prompt | 镜头列表 + Prompt | **六层金字塔：宏观→中观→微观→设定→生图→生视频** |
| 视觉一致性 | 不保证 | 共享视觉主题层 | **角色卡/场景卡/道具卡精确到颜色材质尺寸 + 风格预设库自动匹配** |
| 镜头语言 | 无指导 | 基础构图建议 | **四类镜头语法体系 + 情绪→镜头映射速查表** |
| 声音设计 | 不覆盖 | 基础音频方向 | **每个镜头独立声音设计：环境音/Foley/BGM/旁白** |
| 协作模式 | 一次性 | 一次性 | **Mode B 逐模块确认——每步审阅后才继续** |
| 知识底座 | 无 | 无 | **镜头语法参考 + 23 种风格预设 + 10 种情绪映射** |
| 图生视频 | 不覆盖 | 不覆盖 | **运动描述/表情时间线/运镜指令/音频对齐点** |

---

## 📦 Installation

### Qoder

将本仓库克隆或复制到 Qoder 的 skills 目录：

```bash
git clone https://github.com/your-username/storyboard-director.git ~/.qoder/skills/storyboard-director
```

然后在对话中提及分镜/故事板/视频制作即可自动触发。

### Claude Code

```bash
# 用户级（所有项目可用）
mkdir -p ~/.claude/skills/storyboard-director
cp SKILL.md ~/.claude/skills/storyboard-director/
cp -r story-framework visual-design ai-generation examples ~/.claude/skills/storyboard-director/
```

调用方式：
```
使用 storyboard-director 技能，为我的故事生成分镜脚本
```

### Cursor

将 `SKILL.md` 的内容（不含 YAML frontmatter）追加到项目的 `.cursorrules` 文件中。

### 其他平台

本 Skill 遵循 [Agent Skills 开放标准](https://agentskills.io)，兼容任何支持 `SKILL.md` 格式的 Agent 平台（Codex、Windsurf、Gemini CLI 等）。

---

## 🎯 Use Cases

- 🎬 **视频创作者**：拍短片/广告/宣传片前做分镜策划
- 🤖 **AI 视频创作者**：用 Sora/Seedance/Kling/Runway 等工具时，生成配套的完整 Prompt 管线
- 📝 **编剧/策划**：快速将故事梗概转化为可拍摄的剧本大纲
- 🎓 **影视教学**：展示从故事到分镜的完整拆解流程
- 🎮 **游戏/动画**：过场动画的前期分镜设计
- 🏢 **品牌/营销**：短视频广告的批量创意策划

---

## 📁 Skill Architecture

```
storyboard-director/
├── SKILL.md                     # 工作流总纲（120 行，Agent 入口）
├── LICENSE                      # MIT
├── .gitignore
├── README.md                    # 本文件（人类可读）
│
├── story-framework/             # 模块一至三：故事骨架
│   ├── 01-macro-timeline.md     #   宏观时间轴
│   ├── 02-meso-scenes.md        #   中观场面序列
│   ├── 03-micro-shots.md        #   微观蒙太奇分镜
│   └── reference/
│       └── camera-grammar.md    #   镜头语法知识底座（景别/角度/运镜/焦点 + 情绪映射表）
│
├── visual-design/               # 模块四：视觉设定
│   ├── 04-visual-bible.md       #   总纲：提取规则 + 风格匹配 + 输出顺序
│   ├── characters/
│   │   ├── characters.md        #     人类角色卡模板
│   │   └── character-animal.md  #     动物角色卡模板
│   ├── scenes.md                #   场景卡模板
│   ├── props.md                 #   道具卡模板
│   └── styles/general/          #   视觉风格预设库（23 种）
│       ├── cinematic-real.md    #     电影写实类（6 种）
│       ├── animation.md         #     动画类（5 种）
│       ├── painterly.md         #     绘画类（6 种）
│       └── stylized.md          #     风格化（8 种）
│
├── ai-generation/               # 模块五至六：AI 生成
│   ├── 05-text-to-image.md      #   文生图 Prompt 设计
│   └── 06-image-to-video.md     #   图生视频动作序列
│
├── examples/                    # 示例输出
│   └── tennis-girl/             #   网球女孩（3 分钟温情励志）
│       ├── README.md
│       ├── 01-macro-timeline.md
│       ├── 02-meso-scenes.md
│       ├── 03-micro-shots.md
│       ├── 04-visual-bible.md
│       ├── 05-text-to-image.md
│       └── 06-image-to-video.md
│
└── versions/                    # 版本快照（v1.0 ~ v1.4）
```

---

## 🎾 Example: Tennis Girl

完整示例见 [examples/tennis-girl/](examples/tennis-girl/) —— 3分钟温情励志短片，58 个镜头 × 6 模块的完整拆解。

| 指标 | 数值 |
|------|:---:|
| 总镜头数 | 58 |
| 角色数 | 4（小林、退休教练、对手、柴犬） |
| 场景数 | 4 |
| 道具卡 | 8 |
| 风格匹配 | 自然光主义（23 种预设库中自动匹配） |
| 文生图 Prompt | 18 个代表性镜头完整输出 |
| 图生视频动作序列 | 12 个关键镜头详细描述 |

---

## 🤝 Contributing

欢迎贡献！特别欢迎以下方向：

- 🎨 新增风格预设（`visual-design/styles/general/`）
- 📖 新增示例案例（`examples/`）
- 🔧 改进模块指令文件的清晰度和覆盖度
- 🌐 翻译 SKILL.md 到其他语言

提交 PR 前请确保示例案例可正常运行。

---

## 📄 License

MIT — 自由使用，商业或个人项目均可。详见 [LICENSE](LICENSE)。
