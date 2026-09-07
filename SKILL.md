# MiniMax H3 MV 对口型生成技能

## 技能名称
`minimax-mv-lipsync`

## 技能描述
基于 MiniMax H3 视频生成模型的数字人对口型 MV 批量生产技能。支持 MV 唱歌对口型、讲解口播、脱口秀三大内容分支。自动按 SRT 气口切段，生成六段式英文提示词和 `dtmv:v1` 时间线，直连 ComfyUI 批量生产。

## 触发条件
当用户提到以下内容时触发：
- "做 MV"、"对口型"、"数字人唱歌"
- "H3 提示词"、"MiniMax 分镜"
- "批量生成视频"、"dtmv 时间线"

## 输入要求

### 必选
1. **音频总时长 T** — 精确到一位小数秒
2. **SRT / VTT 字幕** — 带时间轴的歌词或台词
3. **内容类型** — MV / 讲解 / 脱口秀
4. **角色参考图** — 至少 1 张主角参考

### 可选
- 场景参考图
- 画幅比例（默认 16:9）
- MV 子类型：剧情向 / 画面向
- 整体氛围描述

## 输出内容

1. **dtmv:v1 时间线** — 直接粘贴 ComfyUI DTMV 节点
2. **分镜地图** — 逐段逐镜头，含景别/运镜/情绪
3. **六段式提示词** — 每段完整英文提示词
4. **角色设计手册** — 记忆点/人设/标志性动作

## 工作流程

### Step 1: 分析与切段
- 读取 SRT，分析歌词/台词内容
- 按气口切段（3-15 秒/段，精度 0.1 秒）
- 生成 `dtmv:v1` 时间线字符串

### Step 2: 角色设计
- 每人 3 个强记忆点
- 前世今生版本需设计命运呼应
- 输出三视图规格：16:9 白底，左 1/3 面部特写，右 2/3 正侧后

### Step 3: 分镜设计
- 每段 4-6 个镜头
- 8 大运镜手法：缓推/环绕/升降/横移/匹配剪辑/闪白/手持/叠化
- 情绪曲线设计

### Step 4: 提示词生成
- 六段式结构：subject_definitions / retention_analysis / Look / Timeline / Editing rules / Audio Text
- 每段硬切转场，禁止溶解叠化（指定除外）
- 严格禁止任何字幕/文字叠加

## 六段式提示词模板

```
subject_definitions:
[角色+场景的英文定义，参考图标签]

retention_analysis:
[角色特征保留分析]

Look:
[画面风格/光影/色调/画质]
Bottom of the frame empty: no bar, no strip, no lower third.

Timeline:
Xs - [镜头描述]
Hard cut:
Ys - [镜头描述]

Editing rules:
Hard cuts only, no dissolves. No burnt-in text of any kind.

Audio / Text:
No burnt-in text of any kind. Forbidden: subtitle bar, closed captions, karaoke...
```

## 参考图标签规范

```
<image 1> = 角色1
<image 2> = 角色2
<image 3> = 角色3
<image 4> = 角色4
<image 5> = 场景1
<image 6> = 场景2
```

## 运镜手法速查

| 运镜 | 英文描述 | 情绪作用 |
|---|---|---|
| 缓慢前推 | slowly pushing forward | 凝神聚焦 |
| 环绕 | slow orbital / 360-degree arc | 命运感·仪式感 |
| 升镜 | camera crane up / rising | 升华·开阔 |
| 降镜 | craning down / descending | 收束·落地 |
| 横移 | trucking / tracking sideways | 流动·推进 |
| 匹配剪辑 | match cut | 命运呼应 |
| 闪白 | flash frame / white flash | 冲击·时空断裂 |
| 手持晃动 | handheld with slight sway | 真实·动荡 |

## 注意事项

1. 所有提示词**严禁包含任何字幕文字**
2. 画面底部保持空白，无任何文字条
3. 转场以硬切为主，叠化需明确指定
4. 角色一致性需在 retention_analysis 中明确说明
5. 参考图标签从 `<image 1>` 开始编号
