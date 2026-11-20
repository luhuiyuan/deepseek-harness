# AI 驱动画图项目调研记录

> 调研日期：2026-11-20
> 调研目的：寻找「用 AI 读懂代码 → 在画布上绘制业务流程图 / 架构图，最好带动画」的前端项目，作为后续深入研究的候选清单。
> 说明：本文记录的是调研快照，star 数、版本号会随时间变化，请以 GitHub 仓库实时数据为准。文中标注 ✅ 的仓库地址已二次核实。

---

## 一、核心需求（选型标尺）

1. **AI 读代码出图**：能读取 GitHub 仓库或本地代码库，生成模块架构图 / 调用链 / 时序图，最好能溯源到 `文件:行号`。
2. **画布可编辑**：不是一次性图片，而是能在无限画布上继续调整、缩放、连线。
3. **动画**：连线流动、节点出现、数据流播放等动态效果，能导出 GIF / MP4 / SVG。
4. **AI 辅助创作**：自然语言描述 → 生成图，或在画布上对话式改图。

按这四点，把项目分成五类，见下面总览。

---

## 二、项目总览

### A. 开箱即用、自带动画的画布应用

| 项目 | 地址 | 亮点 | 匹配度 |
|------|------|------|--------|
| **AIFlow Motion** | `dongou1024/aiflow-motion` | 7 种边动画 + 6 种节点动画 + 10 种图标动画；粒子流动、发光、播放预览；6100+ 品牌 logo；AI 生成工作流；导出 GIF/MP4/WebM/SVG | ★★★★☆ |
| **OpenFlowKit** | `openflowkit/openflowkit` ✅ | 文本与画布双向同步；贴 GitHub 仓库让 AI 画出代码结构图，箭头可点开看 `file:line`；Mermaid/D2 导入；`animate` 导出动画；MCP 服务 | ★★★★★（已在本地部署） |
| **drawcms** | `drawcms/drawcms` | 17 种图表、18 个带动画预设模板；「动画是一等公民」；导出 PNG/GIF；local-first、无需账号 | ★★★★☆ |
| **orrery** | `Sagargupta16/orrery` | YAML 配置 → 动画架构图（数据包沿连线跑）；官方 AWS/Azure/GCP/K8s 图标；导出 draw.io / React 组件 | ★★★☆☆ |

### B. 画布引擎库（需自己二次开发，动画接示例或自写）

| 项目 | 地址 | 亮点 | 匹配度 |
|------|------|------|--------|
| **React Flow / xyflow** | `xyflow/xyflow` | React/Svelte 生态最主流（约 38k star）；无限画布、缩放、自定义节点；官方有 Animated SVG Edge 组件与动画示例；MIT | ★★★★☆（做底子最稳） |
| **LogicFlow** | `didi/LogicFlow` | 滴滴开源，中文文档友好；自带动画折线示例；适合业务流程图 | ★★★★☆ |
| **AntV X6** | `antvis/X6` | 阿里图编辑引擎；流程图 / DAG / 血缘图；支持 React/Vue 定制节点 | ★★★☆☆ |
| **flowmix-flow** | `MrXujiang/flowmix-flow` | 基于 react-flow 的现成工作流编辑器，适合直接改 | ★★★☆☆ |

### C. AI 读代码 → 出图（最贴合「用 AI 了解代码」）

| 项目 | 地址 | 亮点 | 匹配度 |
|------|------|------|--------|
| **GitDiagram** | `ahmedkhaleel2004/gitdiagram` ✅ | 把 `github.com` 换成 `gitdiagram.com` 即出交互式架构图（约 18.6k star，MIT）；每个组件链接到真实源码；导出 PNG/Mermaid；私有仓库用浏览器本地 GitHub token；提供 MCP 服务和 `.md` 版本；新增约 1 分钟解说视频（MP4）；技术栈 Next.js 16 + React 19 + Bun + Cloudflare R2 + Upstash Redis，自部署可切 OpenRouter | ★★★★★（零安装首选） |
| **pr-lens** | `coldteadotai/pr-lens` ✅ | 「最快理解代码」；约 2.4k star；结构化图文档 → 动画架构图 / 数据流图 / 数据模型图；用颜色区分新增/修改/删除；按步骤播放数据流并看载荷；带交互画布；属 Agent Skill，需配套 CLI 校验渲染 | ★★★★☆ |
| **archify** | `tt-a1i/archify` ✅ | 面向编码 Agent 的 Skill（Apache-2.0，star 数各来源差异大，约 1.9 万～9 万）；10 种图（架构/工作流/时序/数据流/生命周期/ERD/类/树/时间线/甘特）；JSON IR → 确定性编译成自包含 HTML；源码溯源、Before/After Delta 对比、原子校验；Claude Code/Codex/Cursor/OpenCode 都能用；一行命令安装：`npx -y skills@latest add https://archify.si --skill archify --agent claude-code --global --copy --yes` | ★★★★★（溯源最强） |
| **architect-skills** | `sirius-zuo/architect-skills` | 架构分析 + 评审 Skill；生成带真实证据的 Mermaid 图 + HTML 报告 | ★★★☆☆ |

### D. 自然语言 → 可编辑图（Excalidraw / draw.io 生态）

| 项目 | 地址 | 亮点 | 匹配度 |
|------|------|------|--------|
| **CanvasAnvil** | `CodingFeng101/CanvasAnvil` | 无限画布 + AI 生成；写可编辑 `.drawio` 文件（self-hosted draw.io 替代）；还能做 AI PPT / 信息图 | ★★★★☆ |
| **OpenDiagram** | `Itz-Agasta/OpenDiagram` | 开源版 Eraser.io；英文描述系统 → Excalidraw 画布上的可编辑架构图；可自托管、自带 key | ★★★★☆ |
| **next-ai-drawio** | `next-ai-draw-io/next-ai-draw-io` | 与 draw.io 深度集成；多轮对话改图、图片转图表 | ★★★★☆ |
| **smart-excalidraw-next** | `liujuntao123/smart-excalidraw-next` | 自然语言生成 Mermaid/Excalidraw/Draw.io 三种格式；20+ 图表类型；国内模型友好 | ★★★★☆ |
| **ArchitextAI** | `DemonDamon/ArchitextAI` | 文字/图片生成流程图 + 信息图；ELK.js 自动布局；支持 DeepSeek/智谱/通义等国内模型；一键美化 | ★★★☆☆ |

### E. 一句话出图的 Skill（无需跑服务）

| 项目 | 地址 | 亮点 | 匹配度 |
|------|------|------|--------|
| **fireworks-tech-graph** | `yizhiyanhua-ai/fireworks-tech-graph` ✅ | 自然语言 → 几何校验的 SVG/PNG（可选语义 GIF）；12 风格、完整 14 种 UML；内置 RAG/Multi-Agent/Mem0/Tool Call 等 AI 模板；Python 渲染器保证稳定；MIT；安装 `npx skills add yizhiyanhua-ai/fireworks-tech-graph` | ★★★★★（出图质量高） |
| **architecture-diagram-generator** | `Cocoon-AI/architecture-diagram-generator` | 输出单个嵌入 SVG 的 HTML，深色主题，方便分享 | ★★★☆☆ |
| **excalidraw-diagram-generator** | `github/awesome-copilot` 的 `skills/excalidraw-diagram-generator` | 生成可编辑 `.excalidraw` 文件 | ★★★☆☆ |
| **diagram-design** | `cathrynlavery/diagram-design` ✅ | 约 36.7k star；编辑向图解 Skill，约 39 种类型，自包含 HTML+SVG；可品牌化配色；支持从 draw.io / Mermaid / Excalidraw 重绘 | ★★★☆☆ |
| **visual-explainer** | `nicobailon/visual-explainer` ✅ | 约 9.7k star；把架构图、diff 评审、计划审计、表格做成整页 HTML 或杂志风幻灯片，偏「一页讲清楚」 | ★★★☆☆ |

> 补充核实到的同类 Skill：`coleam00/excalidraw-diagram-skill`（约 4.7k star，生成可编辑 Excalidraw 图，强调视觉论证与渲染自检）。

---

## 三、按需求场景的推荐

| 你的场景 | 首选 | 备选 |
|----------|------|------|
| 零安装、快速看某个仓库架构 | **GitDiagram**（改域名） | DeepWiki（改域名出 wiki + 问答） |
| AI 读代码且要溯源到行号 | **archify** / **pr-lens** | OpenFlowKit |
| 画布上边聊边改、要动画 | **OpenFlowKit** | drawcms / AIFlow Motion |
| 生成后去 draw.io 精修 | **CanvasAnvil** / **next-ai-drawio** | OpenDiagram |
| 只要高质量静态图放文档 | **fireworks-tech-graph** | diagram-design |
| 自己二次开发画布引擎 | **React Flow** | LogicFlow（中文）/ AntV X6 |

---

## 四、信息修正与注意事项

1. **GitDiagram 地址已修正**：先前记录写成 `ahmad Nassar/gitdiagram`（有误），正确为 **`ahmedkhaleel2004/gitdiagram`**。
2. **star 数普遍有出入**：不同来源抓取时间不同，尤其 archify（1.9 万～9.4 万）、fireworks-tech-graph（6.8k～12k）差异较大，选型时请以 GitHub 实时数据为准。
3. **Skill 类 vs 应用类**：pr-lens / archify / fireworks-tech-graph / diagram-design 是 **Agent Skill**（给 Claude Code、Codex、Cursor 等编码 Agent 用），不是独立 Web 应用；OpenFlowKit / drawcms / CanvasAnvil 才是能跑起来的前端应用。
4. **深度对比参考**：GitDiagram 官网有一篇同类工具横评 `https://gitdiagram.com/best-codebase-visualization-tools`（站方自述，注意立场），对比了 GitDiagram / DeepWiki / Sourcegraph / dependency-cruiser / Madge / pydeps / Mermaid / PlantUML / Structurizr。

---

## 五、当前环境中的部署状态

| 项目 | 状态 | 访问方式 |
|------|------|----------|
| **deepseek-harness**（本项目） | 已通过源码安装运行，`research` 分支（与 `master` 同一提交 `2e39e70496`）；Web UI 经反向代理发布到公网 | `https://a2f2a8844eb666f8b.app.workbuddy.host/?sharecode=I44NNF4FES` |
| **OpenFlowKit** | 已通过源码安装并在本地 3000 端口运行（Vite dev），未发布公网 | `http://localhost:3000` |

> 注意：沙箱休眠/重启后进程可能被清理。DSH 已配置统一自启动脚本 `dsh-publish/start.sh` 自动拉起主进程与代理并同步 token；OpenFlowKit 若访问不了需重新执行 `npm run dev`。

---

## 六、后续深入研究建议

1. **先做效果横评**：用本仓库 `deepseek-harness` 作为样本，分别用 GitDiagram（改域名）、archify、OpenFlowKit 各出一张架构图，对比「能否溯源到行号 / 中文支持 / 动画 / 可编辑性」四项。
2. **重点验证 archify**：它对 10 种图的支持和 JSON IR → 确定性 HTML 的机制最工程化，适合长期维护的架构文档；注意其校验只查结构不查语义，图内容仍需人工核对。
3. **国内模型路线**：若要用 DeepSeek / 智谱 / 通义，优先看 **ArchitextAI** 和 **smart-excalidraw-next**；fireworks-tech-graph 也可通过自定义渲染接入。
4. **动画导出**：若要 GIF/MP4，AIFlow Motion 与 OpenFlowKit 的 `animate` 导出最直接；archify 支持导出 WebM；pr-lens 主打 PR 场景的动画表达。
5. **MCP 方向**：OpenFlowKit 与 GitDiagram 都提供 MCP 服务，可让编码 Agent 直接把图「画进」工作流，值得优先试。
