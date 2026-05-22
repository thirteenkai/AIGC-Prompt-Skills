# AIGC Prompt Skills 发布与安装流程

本文档用于固定主仓库、Codex 安装副本和旧 skill 归档之间的关系，避免多处同时修改导致版本混乱。

## 目录职责

| 路径 | 职责 | 是否手动编辑 |
| --- | --- | --- |
| 本地主仓库目录 | 主版本 / 源码仓库 / GitHub 发布源 | 是 |
| `~/.codex/skills/<skill-name>` | Codex 实际加载的安装副本 | 否 |
| `~/.cc-switch/skills` | 旧 skill 来源目录 | 不再编辑 |
| `~/.cc-switch/skills-archive/<date>` | 旧版归档目录 | 否 |

以后所有 skill 修改只在主仓库完成。`~/.codex/skills` 只用于运行，不作为编辑源。

## 当前发布的 Skill

- `image-prompt`
- `video-prompt`
- `aigc-storyboard-video-workflow`

`storyboard-director` 是旧实验版，不发布，只归档。

## 日常编辑流程

```bash
cd "<your-local-path>/aigc-prompt-skills"

# 修改 SKILL.md 或 references 后先检查
find . -name '.DS_Store' -delete
rg -n "飞书|feishu|/Users/|\\.env|token|secret|password|客户|未公开|私人偏好|历史案例|prompt-library" .

git status --short
git add .
git commit -m "Update skills"
git push
```

敏感词扫描有命中不一定都是问题，但必须逐条确认。公开版不应包含内部账号配置、私人偏好、客户信息、历史跑图记录或飞书同步信息。

## 首次推送到 GitHub

```bash
cd "<your-local-path>/aigc-prompt-skills"

git init
git add .
git commit -m "Initial AIGC prompt skills"
git branch -M main
git remote add origin https://github.com/thirteenkai/AIGC-Prompt-Skills.git
git push -u origin main
```

## Codex 安装

推荐先让支持 Skill 的 Agent 直接安装：

```text
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/image-prompt
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/video-prompt
帮我安装这个 skill：https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-storyboard-video-workflow
```

如果要在 Codex 里手动安装，安装前确认目标目录不存在旧副本。如果已存在，先删除对应目录。

```bash
rm -rf ~/.codex/skills/image-prompt
rm -rf ~/.codex/skills/video-prompt
rm -rf ~/.codex/skills/aigc-storyboard-video-workflow

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/image-prompt

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/video-prompt

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/aigc-storyboard-video-workflow
```

安装后重启 Codex 生效。

## 更新 Codex 使用版

每次 GitHub 有新版本后，Codex 使用版不要手动改，直接重新安装：

```bash
rm -rf ~/.codex/skills/<skill-name>

python3 "$HOME/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/thirteenkai/AIGC-Prompt-Skills/tree/main/<skill-name>
```

## 归档旧版

确认 GitHub 推送完成、Codex 新版安装完成后，把旧 `.cc-switch` 重复 skill 归档：

```bash
archive_dir="$HOME/.cc-switch/skills-archive/$(date +%F)"
mkdir -p "$archive_dir"

mv "$HOME/.cc-switch/skills/image-prompt" "$archive_dir/" 2>/dev/null || true
mv "$HOME/.cc-switch/skills/video-prompt" "$archive_dir/" 2>/dev/null || true
mv "$HOME/.cc-switch/skills/aigc-storyboard-video-workflow" "$archive_dir/" 2>/dev/null || true
mv "$HOME/.cc-switch/skills/storyboard-director" "$archive_dir/" 2>/dev/null || true
```

不要删除整个 `~/.cc-switch/skills`，里面还有其他 skill。

## 验证清单

```bash
test -f ~/.codex/skills/image-prompt/SKILL.md
test -f ~/.codex/skills/video-prompt/SKILL.md
test -f ~/.codex/skills/aigc-storyboard-video-workflow/SKILL.md
```

重启 Codex 后分别用以下意图验证触发：

- “帮我把这个图片想法写成提示词”
- “这张首帧图帮我写视频提示词”
- “这段剧情帮我生成故事板提示词”
