# 示例案例：网球女孩

> 本目录展示 storyboard-director v1.4 技能的完整六模块输出结果。
> 
> 输入故事：13岁女孩小林的网球梦想之路。Mode B（逐模块确认）风格输出。

## 输入

- **故事概要**：13岁女孩小林，每天清晨到社区网球场独自练习，梦想成为职业网球选手。从失败到坚持，偶遇退休教练指导，最终在市青少年比赛中获胜
- **核心风格**：温情励志
- **总时长**：3 分钟

## 风格匹配

✅ **自然光主义**（`cinematic-real.md`）— golden hour, natural light, backlit, lens flare, soft shadows

## 各模块概览

| 模块 | 文件 | 角色 | 产出概要 |
|:---:|------|------|---------|
| 一 | [01-macro-timeline.md](01-macro-timeline.md) | 策划总监 | 起/承/转/合四段宏观时间轴，总40"+50"+45"+45"=180s |
| 二 | [02-meso-scenes.md](02-meso-scenes.md) | 执行导演 | 4个时间段拆解为17个场面（地点+核心动作） |
| 三 | [03-micro-shots.md](03-micro-shots.md) | 摄影指导 | 17个场面 → 58个蒙太奇镜头，含景别/运镜/画面/声音完整分镜表 |
| 四 | [04-visual-bible.md](04-visual-bible.md) | 美术指导 | 风格匹配 + 4张角色卡 + 4张场景卡 + 8张道具卡 |
| 五 | [05-text-to-image.md](05-text-to-image.md) | Prompt设计师 | 18个代表性镜头的完整英文Prompt + 中文参考 + 一致性引用 |
| 六 | [06-image-to-video.md](06-image-to-video.md) | 技术指导 | 12个关键镜头的运动描述/表情时间线/运镜指令/音频对齐点 |

## 关键数据

- **总镜头数**：58
- **角色数**：4（小林、退休教练、对手、柴犬）
- **场景数**：4（社区球场/外围小路/市体育馆/观众席）
- **道具数**：8（球拍/网球/发球机/球包/记分牌/水瓶/护腕/狗绳项圈）
- **风格预设**：1（自然光主义，23种预设库中匹配）

## 文件结构

```
examples/tennis-girl/
├── README.md              # 本文件，案例概览
├── 01-macro-timeline.md   # 模块一：宏观时间轴
├── 02-meso-scenes.md      # 模块二：中观场面序列
├── 03-micro-shots.md      # 模块三：微观蒙太奇分镜
├── 04-visual-bible.md     # 模块四：视觉设定资料库
├── 05-text-to-image.md    # 模块五：文生图提示词
└── 06-image-to-video.md   # 模块六：图生视频动作序列
```

---

> 本案例使用 storyboard-director v1.4 生成，展示从故事概要到 AI 生成管线的完整六模块输出。
