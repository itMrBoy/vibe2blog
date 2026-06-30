# 归档

## 路径

`.blog/YYYY-MM-DD/<主题-slug>.md`

- 日期用当天(`date +%Y-%m-%d`)。
- `<主题-slug>`:由主题转成短横线连接的文件名,中文可保留,去掉空格和标点。例:主题"重构 AI Provider 抽象" → `重构-ai-provider-抽象.md`。

## 不静默覆盖

写之前先看目标路径是否已存在:

- 已存在 → 不直接盖。追加序号(`<slug>-2.md`),或问作者要覆盖还是另存。
- 用 `test -f` 判断,别假设不存在。

## frontmatter(最小,仅供检索)

正文前加:

```yaml
---
title: <标题>                  # 自然有劲的标题,见 narrative.md「标题怎么起」
date: 2026-06-30 01:16:33      # 到时分秒,取自 date +"%Y-%m-%d %H:%M:%S"
topic: <主题>                  # 原主题词,用于检索归类,可与 title 不同
source: [对话, git, llmdoc]   # 本篇实际用到的素材源,按需删减
visibility: public            # public | private
---
```

字段只为检索,不是正文模板。

## 正文标题

frontmatter 之后、正文开头放一个 `# 一级标题`,用 frontmatter 的 `title`。正文从标题下一段起。

## 收尾

写完报告落盘的绝对路径,方便作者打开。
