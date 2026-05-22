# AIGC Prompt Skills 组员安装与使用指南

这份文档给组员使用。目标是让大家知道每个 skill 装什么、怎么装、装完怎么触发。

## 一、Skill 列表

| Skill | 用途 | 安装链接 |
| --- | --- | --- |
| `image-prompt` | 图片生成、改图、多图参考、风格迁移提示词 | `https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/image-prompt` |
| `video-prompt` | 首帧 / 首尾帧转视频提示词 | `https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/video-prompt` |
| `aigc-storyboard-video-workflow` | 剧情检查、故事板提示词、故事板审核、视频提示词 | `https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-storyboard-video-workflow` |

## 二、推荐安装方式

在 Claude Code、Codex、OpenClaw 等支持 Skill 的 Agent 里，直接说：

```text
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/image-prompt
```

```text
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/video-prompt
```

```text
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-storyboard-video-workflow
```

安装完成后，重启 Agent / Codex。

## 三、Codex 手动安装方式

如果直接让 Agent 安装失败，可以在终端执行：

```bash
python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/image-prompt

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/video-prompt

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-storyboard-video-workflow
```

安装完成后，重启 Codex。

## 四、怎么使用

### 图片提示词：`image-prompt`

适合：

- 文生图
- 改图 / 修图
- 多图参考
- 风格迁移

可以这样说：

```text
帮我把这个图片想法写成提示词
把这张图的背景改成夜晚街道
把图 2 的画风套到图 1 的角色上
```

### 视频提示词：`video-prompt`

适合：

- 首帧图转视频
- 首尾帧转视频
- 给可灵 / 即梦 / Seedance 写视频提示词

可以这样说：

```text
这张首帧图帮我写视频提示词
让这个角色慢慢转头看窗外
这两张图做首尾帧，帮我写即梦视频提示词
```

### 故事板工作流：`aigc-storyboard-video-workflow`

适合：

- 检查剧情是否足够生成故事板
- 生成 image-2 故事板提示词
- 审核故事板
- 基于故事板生成视频提示词

可以这样说：

```text
这段剧情帮我生成故事板提示词
/检查剧情
/生成故事板提示词
/审核故事板
/生成视频提示词
/完整流程
```

## 五、更新方式

当前没有自动更新机制。收到更新通知后，重新安装对应 skill。

Codex 用户可以执行：

```bash
rm -rf ~/.codex/skills/<skill-name>

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/<skill-name>
```

把 `<skill-name>` 换成：

- `image-prompt`
- `video-prompt`
- `aigc-storyboard-video-workflow`

更新后重启 Codex。

## 六、常见问题

### 安装后没有触发怎么办？

先重启 Agent / Codex。Skill 通常需要重启后才会被重新加载。

### 三个 skill 都要装吗？

建议都装。它们职责不同：

- 图片阶段用 `image-prompt`
- 视频阶段用 `video-prompt`
- 剧情到故事板再到视频的一整套流程用 `aigc-storyboard-video-workflow`

### 可以直接改 `~/.codex/skills` 里的文件吗？

不建议。`~/.codex/skills` 是安装副本，不是编辑源。后续更新以 GitHub 仓库版本为准。
