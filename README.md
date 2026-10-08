# 🎵 YuE2 Music (YuE 2.0 白盒音乐大模型创作平台)

[![Framework](https://img.shields.io/badge/Framework-TanStack%20Start%20%7C%20React%2019-blue.svg)](https://tanstack.com/start)
[![Runtime](https://img.shields.io/badge/Runtime-Vite%208%20%2B%20Nitro%20%2B%20Cloudflare%20Workers-orange.svg)](https://developers.cloudflare.com/workers/)
[![Model](https://img.shields.io/badge/AI%20Model-YuE%202.0%20Foundation%20Music-purple.svg)](https://github.com/multimodal-art-projection/YuE)
[![ORM](https://img.shields.io/badge/ORM-Drizzle%20%28SQLite%20%7C%20D1%29-green.svg)](https://orm.drizzle.team/)
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](LICENSE)

**YuE2 Music** 是基于 M·A·P（Multimodal Art Projection 多模态艺术投影）团队推出的开源前沿音乐基座模型 **YuE 2.0** 构建的全栈白盒 AI 音乐创作平台与 SaaS 系统。

与传统黑盒 AI 音乐生成器（如 Suno、Udio 等“输入提示词直接黑盒输出音频”）不同，YuE2 Music 引入了**思维链符号规划 (Symbolic CoT Planning)**。系统将结构化 **ABC 记谱法 (ABC 2.1 Notation)** 作为白盒中间表征，支持人类音乐家或内置 AI Agent 进行和弦重配、转调、曲式改写，并在浏览器中实现零 GPU 延迟的 Web Audio 实时合成试听，最后交由高性能神经音频扩散流水线渲染输出 48kHz 高保真立体声全曲。

---

## 🌟 核心特性

### 1. 🎼 白盒符号规划与透明可控创作 (White-Box Symbolic Planning)
- **拒绝黑盒抽卡**：模型先规划出明文可读的 ABC 乐谱，包含调性、拍号、速度、和弦走势与分轨旋律。
- **灵活干预与二次编曲**：支持半音阶升降调（Transpose）、八度位移、和弦替换（如流行转爵士七和弦、五声重配、伤感小调重配等）。
- **专业乐谱校验引擎**：内置 ABC 语法自动诊断与容错修复，确保生成的乐谱符合音乐学规范。

### 2. 🎹 交互式编曲工作台 (YuE2 Studio)
- **实时五线/简谱渲染**：集成 `abcjs`，动态渲染标准乐谱视图，支持小节高亮和缩放。
- **浏览器实时音频合成器 (Web Audio Synth)**：在无需等待昂贵 GPU 渲染前，直接在浏览器端实时回放旋律与和弦进行，秒级试听作曲效果。
- **结构化歌词与分段编排**：直观编辑 `[Intro]`、`[Verse]`、`[Chorus]`、`[Bridge]`、`[Outro]`，精准控制人声演唱结构。
- **AI 唱片封面设计**：根据歌曲流派、歌词意境自动生成 Prompt 并调用生图服务生成 4K 专辑封面。

### 3. 🤖 对话式 AI 作曲助手机器人 (Music Composer Agent)
- **自然语言多轮交互**：只需说出需求（如“把副歌改成更激昂的爵士和弦，升一个全音”），Agent 自动解析并调用工具执行编曲修改。
- **丰富的内置 Toolchain**：
  - `transpose`: 精准升降调
  - `reharmonize_jazz / pop / sad_minor`: 风格化和弦重配
  - `change_tempo / change_meter`: 节拍与速度调整
  - `render_audio`: 确认定稿后一键提交 GPU 全曲渲染任务

### 4. 🎧 音频转谱与逆向分析套件 (Audio-to-Score & SheetSage2)
- **Audio to Score** (`/audio-to-score`)：上传任意歌曲录音，自动逆向转录为 ABC 乐谱。
- **Audio to MIDI** (`/audio-to-midi`, `/mp3-to-midi`)：一键提取旋律与伴奏分轨 MIDI，无缝导入 Logic Pro、Ableton Live、FL Studio。
- **Audio to MusicXML** (`/audio-to-musicxml`)：导出标准五线谱 XML 格式，导入 MuseScore / Sibelius / Finale。
- **Audio to Lead Sheet** (`/audio-to-lead-sheet`)：生成旋律和弦总谱 Lead Sheet。
- **Suno 版权与创作指纹固化** (`/suno-copyright`, `/suno-midi-export`)：将 Suno 生成的音频提取 MIDI 与乐谱，形成确凿原创版权链路。

### 5. ⚡ 神经音频扩散流水线 (Neural Audio Rendering)
- **RunPod Serverless 算力集群集成**：连接 GPU Worker 节点，通过流式状态机跟踪任务：
  `QUEUED` ➔ `SYMBOLIC_PLANNING` ➔ `DIT_FLOW_MATCHING` ➔ `VAE_DECODING` ➔ `COMPLETED`
- **48kHz 双声道立体声母带级输出**：端到端输出广播级人声与真实声学伴奏。




https://yue2music.com



## 📄 开源许可与致谢

- 本项目基于 MIT 许可证开源。
- 感谢 **M·A·P (Multimodal Art Projection)** 团队研发并开源的 [YuE / YuE 2.0](https://github.com/multimodal-art-projection/YuE) 基础大模型。
- 感谢 [SheetSage](https://github.com/chrisdonahue/sheetsage) 提供的音乐转录理论与音频逆向支持。
- 感谢 [abcjs](https://github.com/paulrosen/abcjs) 提供的优秀开源乐谱解析渲染引擎。
