# AIGC Prompt Skills

一组用于 AIGC 图片、视频和故事板工作流的 Agent Skills。

这个仓库是公开发布版：不包含内部账号配置、私人偏好、客户信息、历史跑图记录或飞书同步信息。

## Skills

| Skill | 用途 |
| --- | --- |
| `aigc-image-prompt` | 把口语化图片需求、改图需求、多图参考需求转成可复制的中文图片提示词 |
| `aigc-video-prompt` | 把首帧 / 首尾帧图片和粗略动作描述转成中文视频提示词 |
| `aigc-storyboard-video-workflow` | 把短视频剧情描述转成 image-2 故事板提示词，并在故事板通过后生成视频提示词 |

`storyboard-director` 是旧实验版，不在本仓库发布。

## 安装

### 方式一：直接让 Agent 安装（推荐）

在 Claude Code、Codex、OpenClaw 等支持 Skill 的 Agent 里，直接说：

```text
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-image-prompt
```

```text
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-video-prompt
```

```text
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-storyboard-video-workflow
```

装完后重启 Agent 生效。

### 方式二：Codex 手动安装

如果你使用 Codex，也可以直接执行：

```bash
python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-image-prompt

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-video-prompt

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-storyboard-video-workflow
```

安装后重启 Codex 生效。

## 使用

### `aigc-image-prompt`

用于图片生成、改图、多图参考或风格迁移。

触发示例：

```text
帮我把这个图片想法写成提示词
把这张图的背景改成夜晚街道
把图 2 的画风套到图 1 的角色上
```

### `aigc-video-prompt`

用于首帧 / 首尾帧转视频提示词。

触发示例：

```text
这张首帧图帮我写视频提示词
让这个角色慢慢转头看窗外
这两张图做首尾帧，帮我写即梦视频提示词
```

### `aigc-storyboard-video-workflow`

用于把剧情描述转成故事板提示词，并在故事板通过后生成视频提示词。

触发示例：

```text
这段剧情帮我生成故事板提示词
/检查剧情
/生成故事板提示词
/审核故事板
/生成视频提示词
/完整流程
```

## 更新

当前没有自动更新机制。发布新版本后，通知使用者重新安装对应 skill。

Codex 用户可执行：

```bash
rm -rf ~/.codex/skills/<skill-name>

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/<skill-name>
```

然后重启 Codex。

## 发布前检查

发布前至少检查：

```bash
find . -name '.DS_Store' -delete
rg -n "飞书|feishu|/Users/|\\.env|token|secret|password|客户|未公开|私人偏好|历史案例|prompt-library" .
```

命中不一定都是问题，但必须逐条确认。

## 目录结构

```text
.
├── README.md
├── aigc-image-prompt/
│   ├── SKILL.md
│   ├── references/
│   └── tests/
├── aigc-video-prompt/
│   ├── SKILL.md
│   ├── references/
│   └── tests/
└── aigc-storyboard-video-workflow/
    ├── SKILL.md
    └── references/
```
