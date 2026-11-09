# leiming2333

写 Minecraft 启动器、模组和整合包，也给 AI Agent 做插件和 MCP 服务。

## 关于我

GitHub 上叫 leiming2333，Minecraft 中文社区里用「黄焖鸡米饭雷明」和「黄焖鸡大米饭雷明」两个昵称。

2022 年就在 Gitee 上放东西，2023 年 5 月在 CurseForge 发布第一份整合包。GitHub 这个号到 2025 年 12 月才开，所以仓库数量看着不多，产出其实分散在几个平台：GitHub 放源码，CurseForge 和 Modrinth 发模组与整合包，npm 发插件，MC百科维护条目。

GitHub 上目前 12 个公开仓库，6 个原创、6 个 fork。原创的大致两类：Minecraft 的启动器、模组和整合包，以及 AI Agent 的插件和 MCP 服务。日常写 JavaScript 和 TypeScript，Python 用在 MCP 服务和插件里，Java 用在模组那边。

近一年在 GitHub 有 295 次贡献，分布在 66 天里，最长连续 8 天。2026 年 10 月最集中，144 次。

## 最近在做

- 维护「忘却的旋律启动器」，源码版本 1.9.3，最近一次改动在 11 月 9 日。
- 做 `dsh-web-search-lite`，给 DeepSeek Harness 补一套不需要 API Key 的搜索，npm 上已到 1.3.2。
- 10 月在 CurseForge 上架了 Second Chapter 这个小模组。

## 技能与工具

| 方向 | 具体内容 |
| --- | --- |
| 语言 | JavaScript、TypeScript、Python、Java、HTML/CSS |
| 桌面端 | Electron 43、Node.js 26、electron-builder（单文件便携 EXE、NSIS）、Windows / macOS / Linux 三平台构建 |
| 模组开发 | Forge、NeoForge、Fabric、Quilt，TerraBlender / GeckoLib / LDLib 等前置库，CurseForge 与 Modrinth 的版本矩阵维护 |
| AI Agent | MCP 服务端、DSH 插件、多模型接入（GPT-4o、Qwen-VL、Gemini、Claude）、把能力同时做成 MCP 工具和独立 Skill |
| 工程 | GitHub Actions CI、`node --test`、自建构建与工具链校验脚本、Vercel 部署、Cloudflare R2 分发 |

## 代表项目

### [忘却的旋律启动器](https://github.com/leiming2333/The-Melody-of-Oblivion-Remake)

GPL-3.0 · JavaScript / Electron · 16 stars · [官网](https://www.melodyoblivion.xyz)

从零重写的 Electron 版 Minecraft Java 启动器，致敬 2012 年前后流行的同名国产启动器，没有使用原版代码。界面保留了旧版安静紧凑的样子，内部实现换成了现代的下载、账户、Java 运行时和启动流程。

- **账户**：Microsoft 设备代码登录、离线账户、LittleSkin（Yggdrasil）。在线令牌用 Electron `safeStorage` 加密，不进渲染进程；安全存储不可用时拒绝读写在线凭据，离线账户照常可用。
- **下载**：Mojang 官方源与 BMCLAPI 二选一，自动模式会先测速。任务并发、大文件 HTTP Range 分段、SHA-1 校验、取消下载、失败换源重试都在里面。
- **模组加载器**：Fabric、Forge、NeoForge、Quilt 走同一套安装流程，新装 Fabric 时可以顺手勾上版本匹配的 Fabric API。
- **整合包**：Modrinth `.mrpack` 和 CurseForge `.zip`，独立实例目录，支持 overrides；可选文件缺失只警告，必需文件失败才中止。
- **Java**：按版本需求匹配主版本，缺 Java 时能一键下载（优先 Azul JRE，失败切 Adoptium，带进度和取消）。
- **发布**：GitHub Releases 决定版本号与 SHA-256，官网下载走 Cloudflare R2 直链，R2 不可用时回退 GitHub。

渲染进程开了上下文隔离和沙箱、关了 Node 集成；账户和设置原子写入并保留 `.bak`，文件损坏时先尝试恢复而不是静默重置。测试覆盖账户、下载、Java 选择、游戏启动、加载器、整合包、设置和启动器更新。

### Minecraft 模组与整合包

| 项目 | 做了什么 | 平台与数据 |
| --- | --- | --- |
| Gun Fire Survival | 整合包：怪物一天比一天强，靠合成枪械活下来 | [CurseForge](https://www.curseforge.com/minecraft/modpacks/gun-fire-survival) 5.36 万次下载，2023 年 5 月上线 |
| 辐射区 Radiation Area | 新增辐射群系和防辐射服，联动僵尸拓展，配置文件可改防护服参数；前置 TerraBlender | [CurseForge](https://www.curseforge.com/minecraft/mc-mods/radiation-area) 711 次 / [Modrinth](https://modrinth.com/mod/radiation-area) 146 次；Forge 1.18.2、NeoForge 1.20.1 与 1.21.1 |
| 争锋频道：我的世界城 | 把《明日方舟》的「争锋频道」斗蛐蛐玩法搬进来：选区域、选队伍、10 回合自动对战，含竞猜对决与礼物对决两种模式；前置 LDLib | [CurseForge](https://www.curseforge.com/minecraft/mc-mods/rival-channel-minecraft-city) 38 次 / [Modrinth](https://modrinth.com/mod/rival-channel-minecraft-city) 108 次；NeoForge 1.21.1 |
| RPG 天启进化（NeoForge / Fabric） | 同名模组的 NeoForge 与 Fabric 版本，Forge 原作由 wulang666 发布 | [CurseForge](https://www.curseforge.com/minecraft/mc-mods/rpg-rpgae-neoforgefabric) 293 次，2026 年 3 月上线 |
| Second Chapter 第二次生命 | 加了一个注射器道具，可以先自救，也能救其他玩家；前置 GeckoLib | [CurseForge](https://www.curseforge.com/minecraft/mc-mods/second-chapter) 94 次；NeoForge 1.20.1 |

GitHub 上另有 [Gun-Fire-Survival](https://github.com/leiming2333/Gun-Fire-Survival) 仓库，放的是整合包用的 ZenScript 脚本。

### AI Agent 工具链

| 项目 | 说明 | 语言 / 许可 |
| --- | --- | --- |
| [dsh-web-search-lite](https://github.com/leiming2333/dsh-web-search-lite) | DSH 的免密钥联网搜索插件。DuckDuckGo、Bing、百度、360 四家并发查询，轮转交错后按 URL 去重，避免某一家霸占列表前几位；另带网页正文读取。报错会说明下一步怎么处理，比如碰上反爬建议换引擎或配 Key，429 提示额度用尽。npm 上 1.3.2。 | JavaScript / MIT |
| [dsh-dafeiyu-memories](https://github.com/leiming2333/dsh-dafeiyu-memories) | DSH 记忆插件，配一个 CC0 的公开记忆库。8 个工具覆盖提交、检索、统计、导出；本地私有记忆和准备公开的那部分分开处理，公开前强制过滤和匿名化。 | TypeScript / MIT |
| [Vision-Toolkit](https://github.com/leiming2333/Vision-Toolkit) | 多模态 MCP 服务，另有一套不依赖 MCP 的独立 Skill。6 个工具：图像描述与问答、OCR、目标检测、文生图、图像相似度。启动时按可用的 Key 装载提供方，在 GPT-4o、Qwen-VL、Gemini、Claude 之间切换。npm 上 0.7.0。 | Python / MIT |

## 关于 AI

启动器和模组都有 AI 深度参与，公开的地方也都写明了。启动器的发布帖和 B 站简介写的是「用 GPT 写的」，B 站还给视频标了「含 AI 生成内容」；MC百科上几个模组的开发团队一栏，除了本人，还并列着「GLM 程序」「Codex 程序」「ChatGPT 程序」这类名字。

初版由模型生成，之后补的是边界情况：令牌不进渲染进程、账户和设置原子写入并保留 `.bak`、下载失败换源重试、整合包可选文件失败只警告。启动器 2026 年 7 月建仓，11 月走到 1.9.3，自动化测试也是后面一层层补上的。

## 开源贡献

主要给上游项目修边角和补测试：

| 仓库 | 内容 | 状态 |
| --- | --- | --- |
| [sganggs/Stronghold-Protocol](https://github.com/sganggs/Stronghold-Protocol) | WebRTC P2P 公共状态转发（带签名验证和自动回退）；浏览器 E2E 链路打不开时打印启动参数并在 15 秒后判失败；让可选的 WebRTC 测试在非 Windows 上也能跑 | 3 个已合并 |
| [Rongmario/CleanCut](https://github.com/Rongmario/CleanCut) | 修 Forge 1.15+ 上 `startAttack` mixin 的 redirect 注入错误 | 已合并 |
| [Bluelgin/AutoFTBQ](https://github.com/Bluelgin/AutoFTBQ) | 自定义 API 完整地址开关、生成任务书时保存进度、缓解 Defender 误报，以及一次兼容性修复 | 1 个已合并 |
| [farion1231/cc-switch](https://github.com/farion1231/cc-switch) | 设置页加一组 Codex 修复工具：插件商店和 `auth.json` | 待评审 |

累计提过 19 个 PR，其中 9 个已合并。

## 在各平台

| 平台 | 账号 | 内容 |
| --- | --- | --- |
| GitHub | [leiming2333](https://github.com/leiming2333) | 启动器、模组源码、Agent 插件、MCP 服务 |
| CurseForge | [leiming2333](https://www.curseforge.com/members/leiming2333/projects) | 4 个模组 + 1 个整合包，累计约 5.47 万次下载 |
| Modrinth | [leiming2333](https://modrinth.com/user/leiming2333) | 辐射区、争锋频道 |
| npm | [leiming2333](https://www.npmjs.com/~leiming2333) | `vision-toolkit`、`dsh-web-search-lite` 两个包 |
| Gitee | [leiming2333](https://gitee.com/leiming2333) | 模组源码、NapCat + LangBot 一键部署脚本、DSH 插件 fork |
| MC百科 | [黄焖鸡大米饭雷明](https://center.mcmod.cn/644823) | 4 个模组条目，65 次编辑、5,169 字节 |
| MCBBS 纪念版 | [黄焖鸡米饭雷明](https://www.mcbbs.co/space-uid-209111.html) | 启动器发布帖 |
| 哔哩哔哩 | [黄焖鸡大米饭雷明](https://space.bilibili.com/3690996638419687) | 启动器演示视频 |
| 官网 | [melodyoblivion.xyz](https://www.melodyoblivion.xyz) | 启动器下载与使用说明 |

## 数据一览

| 指标 | 数值 |
| --- | --- |
| GitHub 公开仓库 | 12 个（6 原创，6 fork） |
| 近一年 GitHub 贡献 | 295 次，覆盖 66 天，最长连续 8 天 |
| 提交的 PR | 19 个，9 个已合并 |
| 自有仓库代码构成 | JavaScript 约 77%，Java 约 7%，TypeScript 约 6%，Python 约 3% |
| CurseForge 累计下载 | 约 5.47 万次（含整合包 5.36 万） |
| npm 包 | 2 个，`vision-toolkit` 0.7.0、`dsh-web-search-lite` 1.3.2 |
| 账号起始 | Gitee 2022-07，CurseForge 2023-05，MC百科 2023-06，Modrinth 2023-10，GitHub 2025-12 |

## 联系方式

- **GitHub**：主仓库 [The-Melody-of-Oblivion-Remake](https://github.com/leiming2333/The-Melody-of-Oblivion-Remake/issues) 的 Issues 页，或任意 PR 下留言，回复最快。
- **CurseForge / Modrinth**：模组页的评论区，装了模组出问题时贴日志最方便。
- **邮箱**：[leiming23331@outlook.com](mailto:leiming23331@outlook.com)
- **官网**：[melodyoblivion.xyz](https://www.melodyoblivion.xyz)

---

<sub>以上数据整理于 2026 年 11 月 10 日，取自 GitHub API、CurseForge、Modrinth、npm、Gitee、MC百科、MCBBS 与 B 站公开页面。数字会变，需要更新时按同一口径重取。</sub>
