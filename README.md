# AI 内容工作流 Skills

一套面向内容创作者的通用 Codex Skills，覆盖三个彼此独立、又能组合使用的环节：

1. 从高表现素材中总结有证据边界的候选规律。
2. 从指定素材生成可追溯的候选选题。
3. 从 AI 初稿与用户编辑稿的差异中学习写作偏好。

这三个 Skill 不包含特定账号的定位、经历、案例、产品、素材或数据。项目中的数字目录只作为兼容示例；目录结构不同，也会优先按用户指定路径和文件语义适配。

## 包含的 Skills

| Skill | 适合什么时候用 | 不负责什么 |
| --- | --- | --- |
| `viral-pattern-analysis` | 总结爆款规律、更新标题／开头／正文结构规律库 | 不采集素材、不生成选题、不写正文 |
| `topic-generation-workflow` | 根据新素材生成选题、补漏选题、重新审计选题 | 不总结爆款因果、不生成正文、不发布 |
| `writing-preference-learning` | 学习这次改稿、维护候选／当前／停用写作偏好 | 不自动学习普通改稿、不润色正文 |

三个 Skill 分开封装，是为了避免任务混在一起：规律总结只负责证据归纳，选题生成只负责候选题，偏好学习只在用户明确触发时回流。

## 推荐安装方式

把下面这段话复制给 Codex：

```text
请使用 $skill-installer，从下面的 GitHub 仓库安装三个 Skill：
https://github.com/wangguoqing123/ai-content-workflow-skills

需要安装的目录：
- skills/viral-pattern-analysis
- skills/topic-generation-workflow
- skills/writing-preference-learning
```

安装完成后，在下一轮对话或新任务中使用。

只需要其中一个时，把上面列表改成对应目录即可。

## 命令行安装

已经安装 Codex、并且本机有系统自带 `skill-installer` 的用户，可以运行：

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo wangguoqing123/ai-content-workflow-skills \
  --path \
    skills/viral-pattern-analysis \
    skills/topic-generation-workflow \
    skills/writing-preference-learning
```

默认安装位置为 `~/.codex/skills/`。如果同名目录已经存在，安装器会停止，不会直接覆盖。

## 手动安装

1. 下载或克隆本仓库。
2. 找到仓库内的 `skills/` 目录。
3. 将需要的 Skill 文件夹完整复制到本机 `~/.codex/skills/`。
4. 确认每个目录中的 `SKILL.md`、`agents/` 和 `references/` 都被完整保留。
5. 在下一轮对话或新任务中调用。

Windows 用户的默认目录通常是 `%USERPROFILE%\.codex\skills\`。

## 使用方法

### 1. 总结爆款规律

```text
使用 $viral-pattern-analysis，分析当前工作区的高表现素材。
先逐条建立证据底稿，再总结标题、开头和正文结构规律。
```

它会区分：

- 跨作者候选规律；
- 同一作者的重复做法；
- 只能继续观察的单条做法。

重复出现不等于爆款原因；没有普通或低表现对照时，不会输出“必爆公式”。

### 2. 生成可追溯选题

```text
使用 $topic-generation-workflow，完整读取我指定的这批素材，
生成候选选题，并给每条源素材记录明确去向。
```

可以直接提供素材目录、文件清单或批次。如果没有索引，Skill 会在当前工作区内按语义适配，不会跨项目寻找资料。

### 3. 学习这次改稿

```text
使用 $writing-preference-learning，对比这篇 AI 初稿和我的编辑稿，
保存改稿证据，并更新候选写作偏好。
```

一次改稿默认只形成候选偏好。只有用户明确确认候选规则及适用范围后，才会升级为当前写作偏好。

## 建议工作流

```text
高表现素材
  → $viral-pattern-analysis 总结候选规律
  → $topic-generation-workflow 生成候选选题
  → 完成正文并由用户修改
  → $writing-preference-learning 学习本次改稿
```

三个 Skill 可以单独使用，不要求必须按这个顺序运行。

## 使用前需要准备什么

### 规律总结

- 至少两条可完整读取的高表现内容，才能形成候选规律。
- 最好包含平台、作者、标题、正文或转写；图片、评论和互动数据有多少就提供多少。

### 选题生成

- 明确本轮需要处理的素材目录、文件清单或批次。
- 如果有历史选题文件，放在同一工作区中，便于判断真正重复。

### 偏好学习

- 同一篇内容的 AI 初稿。
- 用户真实修改或明确认可的编辑稿。
- 如果存在多组版本，需要明确哪两份互相对应。

## 重要边界

- 不补造缺失的标题、正文、评论、数据、案例或用户观点。
- 不把高表现素材中的共同特征说成爆款因果。
- 不把来源作者的原句、案例、数据和个人经历复制成自己的内容。
- 不自动发布、发送、上传内容。
- 不覆盖原始素材、AI 初稿、用户编辑稿和历史偏好证据。

## 仓库结构

```text
skills/
├── viral-pattern-analysis/
├── topic-generation-workflow/
└── writing-preference-learning/
```

每个 Skill 都包含入口文件 `SKILL.md`、界面信息 `agents/openai.yaml` 和详细执行合同 `references/`。
