# vibe2blog

把 agent 开发、重构、调试的过程,写成一篇聚焦单一主题、少 AI 味的中文技术随笔,按日期归档到仓库的 `.blog/` 下。

记的是过程里的真东西——实现思路、方案取舍、踩过的坑、想通的瞬间,而不是产品文案。

## 写在前面: 项目初衷

AI Coding 代码生产效率极高, 人的阅读精力却是有限的。

而好的架构品味、方案沉淀、实践经验会越来越重要, 因为AI产出的健壮性、鲁棒性取决于你提出的需求, 换句话说你能考虑到的边界、你能提出的实际问题这绝定了AI产出的上限。

每天成千上万行的代码输出, 动辄几十个session, 上百轮chat, 人脑是记不住那么多东西的, 这个时候 blog 的重要性便显现出来了。

这个skill就是协助我们构建人类的memory。

## 两个 skill

- **blog** — 写作主流程:定题 → 采集素材 → 大纲 → 成稿 → 去味 → 归档。默认分步走,在关键处停下来给选项让你拍板;你说"直接出"就一路写到归档。
- **humanize** — 去 AI 味:对一段文本逐条对照清单做审查改写。被 blog 收尾时内联调用,也能单独对任意中文文本用。

两者解耦:blog 管内容,humanize 管语言质感。blog 走到去味那步,直接读 humanize 的清单文件逐条照做——skill 之间不靠"自激活",靠把知识摆成文件、谁需要谁读。

共享交互准则放在插件根目录的 `references/interaction.md`,由 `blog` 从 `../../references/interaction.md` 读取。

## 安装

### Claude

```
/plugin marketplace add /Users/danniel/code/code/Vibe2blog
/plugin install vibe2blog
```

装好后,说"写篇博客讲 X""把这次重构记一篇"之类即可触发 blog。

### Codex

仓库已带 `.codex-plugin/plugin.json`,Codex 会从 `skills/` 发现 `blog` 和 `humanize` 两个 skill。

本地开发态可直接在 Codex 里安装这个插件目录:

```
codex plugin install /Users/danniel/code/code/Vibe2blog
```

如果你的 Codex 版本使用 marketplace 流程,把本仓库作为本地 marketplace/plugin 源加入后再安装 `vibe2blog` 即可。

开发态如果只想免安装使用单个 skill,可以把 `skills/` 下对应目录拷进某个仓库的 `.claude/skills/`。如果要保留插件级共享资料,请连同根目录 `references/` 一起复制,否则 `blog` 的共享引用会断。

## 产物

落到 `.blog/YYYY-MM-DD/<主题-slug>.md`,带最小 frontmatter(title / date 到时分秒 / topic / source / visibility),正文开头一个自然有劲的标题。`.blog/` 默认建议 gitignore。

## 跨平台

整套用 skill,不用 slash command。当前同时提供 Claude 的 `.claude-plugin/` 和 Codex 的 `.codex-plugin/` manifest。交互方式做了平台自适应:Claude 下用 AskUserQuestion 给结构化选项,其他平台退化为带编号的选项。共享准则统一放在插件根目录的 `references/` 下,适合两边一起带走。

## 参考致谢

去 AI 味规范完全自写,条目与表述均为原创,不复用第三方内容。设计思路参考了以下项目,在此致谢:

- [blader/humanizer](https://github.com/blader/humanizer) (MIT) — 写后审查 + 二次改写 + 语气校准的流程思路。
- [OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL](https://github.com/OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL)、[Humanizer-zh](https://github.com/op7418/humanizer-zh) — 中文去 AI 味的反模板思路。

致谢只落在本 README,不写进任何 skill 内部——skill 内部是给模型读的工作指令,不掺元信息。
