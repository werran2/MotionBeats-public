# Changelog

All notable public beta changes for MotionBeats will be recorded here.

## 5.82 — 2026-11-15

[Download v5.82](https://github.com/werran2/MotionBeats-public/releases/tag/v5.82)

**5.82 / build 582 · Android 9+ · ARM64 (`arm64-v8a`) · debug-signed test build**

This is the next public Android beta after [v1.34](https://github.com/werran2/MotionBeats-public/releases/tag/v1.34). The summary below covers the cumulative changes through 5.82; intermediate development versions were not separate public GitHub releases.

## Read before installing / 安装前必读

**The signing certificate has changed since the public v1.34 APK. Android will not install 5.82 over that APK.** Export your voice packs and save any other important data outside the app before considering uninstalling v1.34. Uninstalling deletes local app data, including settings and history; exported packs do not constitute a complete backup. If you need to retain data that cannot be exported, keep the old installation until you have a suitable migration path. There is no verified automatic migration across these differently signed APKs.

**5.82 与公开 v1.34 APK 的签名证书不同，无法直接覆盖安装。** 如需换装，请先导出语音包，并将其他重要数据另存到 App 外。卸载旧版会删除本地设置、历史记录等数据；导出的语音包不是完整备份。若有无法导出且需要保留的数据，请先保留旧版。本次未验证跨签名自动迁移。

- Download the `.apk` for installation, or the `.zip` containing the same APK. You only need one. Check `SHA256SUMS.txt` if desired.
- 本次附件为 **ARM64 调试版测试包**，需要 Android 9 或更高版本；ZIP 内是同一个 APK，二选一即可。它不是面向生产加固的 release 构建。
- Cloud dialogue and voice generation require a compatible account/service and network access. Local speech models require additional downloads, storage and a capable device; local speech does not make cloud AI dialogue offline.
- 云端对话和语音生成需要相应账户、服务和网络；本地语音模型需额外下载并占用存储，对设备有要求。本地识别/合成不代表云端 AI 对话可以离线。

## 中文：v1.34 → v5.82 累计更新

### AI 对话与角色

- 从动作语音播放扩展为包含 AI 对话、角色管理、语音生成和设置的多页面应用。
- 新增多角色与独立聊天记录、角色开场白、用户资料和对话上下文设置，完善切换角色、返回聊天、清空记录和停止请求的行为。
- 支持 SillyTavern 角色卡导入/导出，保留角色资料和头像，改善卡片模板、宏及提示文本处理。
- 增加流式回复与分段朗读，提供全文/对话文本等朗读过滤设置，减少标记文本被直接读出；修复取消后继续朗读、重复播放、短回复及队列衔接问题。

### 语音输入、实时对话与自定义音色

- 新增按住说话及实时语音对话，完善麦克风授权、识别服务选择、识别结果去重、句末提交、连续轮次和停止后的恢复。
- 提供系统识别与本地识别路径及相关设置，改善不同 Android 语音服务的适配，并加入语音识别诊断记录、导出和上传入口，便于反馈兼容性问题。
- 完善系统、云端及本地 MOSS 语音合成选择、参考音频导入/录制和角色自定义音色；改善模型安装、下载进度、镜像可达性及兼容模型下载。
- 优化本地合成线程策略、预热、首段朗读和连续播放衔接；实际速度、内存及发热仍取决于设备、模型和设置。
- **实时语音边界：**“稳定”和“交互”模式仍按轮次对话，AI 实际播放时暂停监听/提交，再于播放结束或无音频窗口恢复。Android“即时”全双工/播放中打断仍为实验功能，受调试与设备验证条件限制，不作为默认开放且全面验收的能力宣传。

### 动作响应与语音包

- 在原有 IDLE / MILD / MED / HOT 基础上新增 **MAX 档**、触发延迟设置与对应播放槽位；MAX 音频通过本地上传配置，暂不支持云端生成。
- 持续完善强度衰减、触发默认值、连续响应、冷却及播放状态处理；改进调参滑块和档位界面。
- 完善语音包导入/导出、大体积 ZIP、旧格式兼容、音频时长保存、单条替换及生成音频保存到有效语音包的流程。
- 5.82 重点修复索引写入和 Android 中断替换恢复：避免写入中断损坏索引、提交后误删新音频或参考音频；恢复和修改同一个包时保持一致，并为清理失败保留重试依据。

### 云服务、账户与可靠性

- 更新正式云服务对接，完善登录会话、参考音频上传、整包/单条语音生成、任务轮询、取消和下载流程。
- 将排队、账户/计费配置、网络及生成失败分类为更清楚的提示，避免向用户直接显示底层音频错误。
- 改善临时刷新失败时的会话保留、Android 凭证安全存储、服务地址与凭证边界、文件操作范围和下载限制。
- 5.82 同步 Cookie/CSRF 访问，稳定未知 API 错误分类；播放计时改用单调时钟，避免系统时间调整干扰播放节奏，并补充播放与恢复回归测试。

### 界面、本地化与 iOS 进展

- 持续完善十种语言（英语、简体中文、繁体中文、日语、韩语、法语、德语、西班牙语、葡萄牙语、俄语）的界面、错误提示和语言偏好；语言切换在 v1.34 已提供，本次是覆盖与质量的持续改进。
- 调整导航、角色列表、聊天气泡、语音操作、系统边距和设置布局，减少拥挤和状态不一致。
- 同期 iOS 持续追齐对话、角色卡、本地 ONNX 语音、实时语音、MAX 档及语音包管理；5.82 源码还修复了语音数据删除失败反馈与生成任务清理顺序。**本次 GitHub Release 仅提供 Android 附件，不发布 iOS 安装包，也不声明 5.82 iOS 真机验收完成。**

## English: cumulative changes from v1.34 to v5.82

- **AI chat and characters:** Expanded the app beyond motion playback with dedicated chat, character, generation and settings screens. Added multiple characters, separate histories, opening messages, user profiles and context controls, plus SillyTavern card import/export with metadata and avatars. Improved templates, macros, chat persistence and cancellation.
- **Streaming speech:** Added streaming replies and segmented reading with text filters. Improved short replies, queue transitions, cancellation and duplicate-playback handling. Expanded system/cloud/local MOSS speech options and custom character voices using imported or recorded reference audio.
- **Voice input and realtime conversations:** Added press-to-talk and realtime voice, system/local recognition choices, permission handling and Android speech-service adaptation. Improved finalization, repeated-result handling and multi-turn recovery. Added speech-recognition diagnostic capture, export and upload tools.
- **Realtime limits:** Stable and Interactive modes remain turn-based: listening/submission pauses during actual AI playback and resumes after playback or in audio-free windows. Android Instant/full-duplex interruption remains experimental and subject to debug/device-evidence gates; it is not presented as a universally validated default feature.
- **On-device speech models:** Improved model installation, download progress, reachable mirrors and compatible model downloads. Added device-aware synthesis thread policies and work on warm-up and speech-start latency. Performance and resource use vary by hardware and model; local speech processing does not make cloud dialogue offline.
- **Motion response:** Added the MAX intensity tier, trigger-delay setting and playback slot alongside IDLE/MILD/MED/HOT. MAX audio is configured by local upload, not cloud generation. Improved intensity decay, trigger defaults, continuous response, cooldown/playback state and tuning controls.
- **Voice packs:** Improved large-ZIP and legacy imports, duration metadata, individual audio replacement and saving generated entries to valid packs. Version 5.82 adds atomic index writes and interrupted-replacement recovery on Android, protecting committed audio/reference files and retaining retry information after cleanup failures.
- **Cloud generation and accounts:** Updated the production-service integration and refined sign-in/session refresh, reference uploads, full-pack/single-entry generation, polling, cancellation and downloads. Added clearer queue, account/billing, network and generation errors. Improved secure credential storage, server-origin boundaries, file containment and bounded downloads.
- **5.82 reliability fixes:** Synchronized Cookie/CSRF access, stabilized unknown API error classification, switched playback timing to a monotonic clock, and added playback/recovery regression coverage.
- **UI and localization:** Refined navigation, chat density, character lists, voice controls, system insets and settings. Continued improving ten app languages and localized errors; language switching already existed in v1.34.
- **iOS development:** Continued parity work on chat, cards, ONNX speech, realtime voice, MAX and pack management, plus 5.82 deletion-error and generation-cleanup fixes. This release distributes Android binaries only; it does not certify completion of the 5.82 iOS device checks.

## Development milestones / 开发版本里程碑

These group the intervening development versions, rather than claiming a separate public release for every build. / 以下归纳期间开发版本，并不表示每个版本都曾公开发布。

| Version range | Cumulative milestone / 累计里程碑 |
| --- | --- |
| 2.0–2.23 | AI chat, characters and cards, MOSS delivery, UI and localization / AI 对话、角色卡、本地合成模型交付、界面与本地化 |
| 2.33–2.64 | Dialogue errors, streaming read filters and realtime voice entry / 对话错误、流式朗读过滤、实时语音入口 |
| 2.86–3.34 | Realtime pipeline stabilization, Android recognition settings and microphone permission fixes / 实时语音稳定性、Android 识别设置、麦克风权限修复 |
| 3.35–3.84 | Custom voices, playback/recording and queue fixes, large voice ZIP imports / 自定义音色、播放录音与队列修复、大体积语音 ZIP 导入 |
| 3.94–4.10 | Startup latency work, local synthesis thread policies, speech-service selection and intensity decay / 启动延迟优化、本地合成线程、识别服务选择、强度衰减 |
| 4.20–4.54 | Realtime mode boundaries, recognition diagnostics, generation save/error handling / 实时模式边界、识别诊断、生成保存与错误处理 |
| 4.55–5.00 | Experimental interruption/echo-handling research, voice-profile controls, audio/session lifecycle fixes and chat insets / 实验打断与回声处理、声纹清除入口、音频会话修复、聊天边距 |
| 5.20–5.42 | Compatible speech-model downloads, MAX tier and decoder lifecycle work / 兼容语音模型下载、MAX 档、解码生命周期整理 |
| 5.52–5.72 | Account/security, file/download containment, chat persistence, cancellation and audit fixes / 账户安全、文件下载边界、聊天持久化、取消与审查修复 |
| 5.82 | Pack index/recovery fixes, Cookie/CSRF synchronization, playback timing and error handling / 语音包索引恢复、会话同步、播放计时与错误处理 |

## Package verification / 附件校验

Both APK signatures verify cryptographically. Their certificate SHA-256 fingerprints differ:

- Public v1.34: `d6ede4faa7edfcb3c9048cb71b69913c5826b72ab4a2ff6884835ac3cdc729b9`
- This v5.82: `4d092d12bbcfe1afd2b52f2c312764fdf7c7838d4e8b05b1f0aec92b8c7b108c`

The ZIP contains exactly the attached APK, with matching SHA-256. / ZIP 仅包含同名 APK，内外 APK 的 SHA-256 一致。

```text
cb853b76cb7849e1d3deaa9fce62ac6c196737a3e1232157dacc82b74dc39888  MotionBeats-5.82-582-android-arm64-debug.apk
6f384c2d8d55843e1e100ae0e31f77e00e190a60cde0949e5cf10f3e9aced28e  MotionBeats-5.82-582-android-arm64-debug.zip
```

Please report issues with the app version, Android/device model, reproduction steps and an appropriately redacted diagnostic report: [GitHub Issues](https://github.com/werran2/MotionBeats-public/issues). / 反馈时请附版本、设备、复现步骤和已去除隐私信息的诊断材料。


## 1.34 — 2026-05-18

See the [original v1.34 release notes](https://github.com/werran2/MotionBeats-public/releases/tag/v1.34) for the previous public Android beta.

## 1.01

- Current Android version reference.
- Motion-triggered playback with `IDLE`, `MILD`, `MED`, and `HOT` slots.
- Voice pack import and export.
- Local audio upload into voice packs.
- Cloud voice generation flow for beta testing.
- Trigger tuning and continuous response controls.

## Earlier Builds

Earlier builds were internal development builds and are not documented in this public changelog.
