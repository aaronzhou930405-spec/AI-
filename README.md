🎬 AI Video Generator — Text to Movie Pipeline
一个端到端 AI 自动视频生成系统：输入文本，一键生成完整短视频（自动分镜 + 文生图 + 图生视频 + 自动剪辑）。
🚀 项目简介
本项目旨在构建一个“AI 自动导演系统”，将自然语言输入自动转换为可播放的视频内容。
系统会自动完成以下流程：
文本输入
   ↓
故事理解（LLM）
   ↓
自动分镜（Scene Planning）
   ↓
角色与场景一致性控制
   ↓
文生图（Text → Image）
   ↓
图生视频（Image → Video）
   ↓
自动剪辑（FFmpeg / MoviePy）
   ↓
最终视频输出
🎯 项目目标
一句话生成短视频
自动生成电影级分镜
保持角色一致性（Character Consistency）
支持多风格视频生成（科幻 / 纪录片 / 动画 / 广告）
可扩展为 AI 视频生成 SaaS
🧠 核心设计思想

本项目基于“电影工业流程”拆解 AI 生成任务：

1️⃣ 故事生成（Story Understanding）

将输入文本转为结构化 JSON：

故事主题
场景列表
情绪变化
镜头语言
2️⃣ 自动分镜（Scene Planner）

将故事拆解为可执行镜头：

每个 scene = 一个画面
明确 camera movement
保持时间轴一致性
3️⃣ 角色一致性系统（Character System）

解决 AI 视频最大痛点：

同一个角色在不同镜头中保持外观一致

实现方式：

Character Sheet（角色卡）
Prompt injection
Reference image conditioning（IP-Adapter / ControlNet）
4️⃣ 文生图（Text → Image）

用于生成每个镜头的关键帧：

支持模型：

Stable Diffusion XL
DALL·E
Midjourney API（可选）
5️⃣ 图生视频（Image → Video）

将静态关键帧转为动态视频：

AnimateDiff
Stable Video Diffusion
Runway Gen-2 API
6️⃣ 自动剪辑（Auto Editing Engine）

使用 FFmpeg / MoviePy：

功能包括：

镜头拼接
转场效果（fade / zoom）
BGM 自动匹配
字幕生成
节奏控制
🏗️ 系统架构
                 ┌──────────────┐
                 │  User Input  │
                 └──────┬───────┘
                        ↓
             ┌────────────────────┐
             │  LLM Story Engine  │
             └────────┬───────────┘
                      ↓
        ┌────────────────────────────┐
        │  Scene & Shot Planner     │
        └────────┬───────────────────┘
                 ↓
     ┌──────────────────────────────┐
     │ Character Consistency Layer   │
     └────────┬─────────────────────┘
              ↓
     ┌──────────────────────────────┐
     │ Text → Image Generator       │
     └────────┬─────────────────────┘
              ↓
     ┌──────────────────────────────┐
     │ Image → Video Generator      │
     └────────┬─────────────────────┘
              ↓
     ┌──────────────────────────────┐
     │ Auto Video Editor (FFmpeg)   │
     └────────┬─────────────────────┘
              ↓
        🎬 Final Video Output
        📁 项目结构
        ai-video-generator/
│
├── backend/
│   ├── story_engine.py        # LLM故事生成
│   ├── scene_planner.py       # 分镜拆解
│   ├── character_system.py    # 角色一致性
│   ├── prompt_engine.py       # Prompt优化
│   ├── image_generator.py     # 文生图
│   ├── video_generator.py     # 图生视频
│   ├── editor.py              # 自动剪辑
│
├── frontend/
│   ├── web_ui.py (Streamlit / Next.js)
│
├── assets/
│   ├── images/
│   ├── videos/
│
├── pipeline.py                # 主流程入口
├── config.yaml
├── requirements.txt
└── README.md
⚙️ 技术栈
🧠 AI 模型
GPT-4 / GPT-5 / Claude / DeepSeek
Stable Diffusion XL
AnimateDiff
Stable Video Diffusion
🎥 视频处理
FFmpeg
MoviePy
🧩 后端
Python
FastAPI（可选）
🖥 前端
Streamlit（MVP）
Next.js（产品化）
🔥 MVP（最小可行版本）

第一阶段目标：

输入一句话 → 输出 10 秒短视频

流程：
LLM生成3个scene
每个scene生成1张图
每张图转2秒视频
FFmpeg拼接
输出 mp4
💡 核心难点
1. 角色一致性
Character embedding
Reference image conditioning
2. 场景连贯性
Scene memory
Prompt chaining
3. 镜头语言（电影感）
wide shot
close-up
tracking shot
cinematic lighting
4. 时间轴控制

所有 scene 进入 timeline：
[
  {"scene": 1, "duration": 3},
  {"scene": 2, "duration": 4}
]
🚀 未来扩展方向
AI广告生成系统
抖音短视频自动生成
小说 → 动画视频
企业宣传片自动生成
SaaS化平台
📌 项目愿景

让任何人都能像写文字一样制作电影。

🤝 贡献方式

欢迎提交：

Prompt优化方案
Video pipeline优化
新模型接入
UI/UX改进
📜 License

MIT License
