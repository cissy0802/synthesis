# Cross-Site Synthesis · 跨站合成

BigCat's Learning Hub 的合成长文站 —— **把存量变成网络,而不是继续加长列表**。

线上:<https://hub.cissychen.com/synthesis/> · [English](https://hub.cissychen.com/synthesis/index.en.html)

## 这是什么

普通内容站回答「X 是什么」;合成文回答「**X 这个东西,在我这几个站里分别是什么,以及它们为什么对不上**」。每篇的源材料**全部来自本 Hub 已发布的页面**,每一节都深链回源页——读者可以顺着链接钻回去,存量因此变成一张网。

## 已发布

| # | 标题 | 体裁 | 源页 |
|---|------|------|------|
| Syn 1 | [熵:一个词,五个房间](entropy.html) · [EN](entropy.en.html) | A | 10 篇 / 6 站 |

## 仓库结构

- `TOPICS.md` —— 路线图与写作约定(17 篇的选题清单、选题硬门槛、三种体裁)。**人类维护,routine 只读**
- `index.html` / `index.en.html` —— 双语落地页,新文章必须登记进去,否则成孤儿页
- `{slug}.html` / `{slug}.en.html` —— 文章本体,手写双语,无自动同步机制
- `synthesis-map.json` —— 每篇引用的源页路径登记表,供日后的反向链接注入使用

## 与其他仓的不同

这个站由**本地 routine 周更**(`~/.claude/scheduled-tasks/weekly-synthesis/SKILL.md`,每周四 09:00 本地时间),和 `deep-research` 同一套机制——**不是云端 trigger**。写作规则全在那份 SKILL.md 里,仓内不放第二份。

为什么必须本地跑:合成文的前提是**真读了源页**,而云端沙箱访问 `hub.cissychen.com` 整站 403、`api.github.com` 也被挡;本地才能直接读 `~/Desktop/repos/` 下的各个源仓。

它不是日更,所以 hub 首页那张卡片显示徽章而非 commit 日期,也不纳入 `verify-routine-caps` 的浮动封顶引擎。没有 `publish.sh` 闸门、没有 `.maxchars`,页尾的共享脚本硬写在页面里(与 `deep-research` 同样处理)。

搜索索引由 hub 仓的 `build-search.yml` 覆盖(本仓在它的 clone 循环里);hub 首页的入口卡片在 `generate_hub.py` 的 `SYNTHESIS_CARDS`,是整个站一张卡,加新文章不用动它。
