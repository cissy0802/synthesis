# FRESHNESS — hub-coverage-audit

体检日期：2026-10-01 · 覆盖式文件，只保留最新一次。
生成者：`hub-coverage-audit`（本地只读体检）。本次**没有改任何稿子或登记表**。

---

## 1. 登记缺口

**38 个已上线的内容站六处登记全齐。** 脚本报了 2 个 ❌，但查下来两个都还不是上线的站，不算漏登记：

| 仓 | 脚本报缺 | 实际状态 | 建议 |
|---|---|---|---|
| `podcast-deepread` | hub 卡片、搜索索引、sitemap、caps 守卫 | **还没出生**：本地 `main` 一个提交都没有，GitHub 上也没有这个仓（`gh api` 404）。目录里只有 `TEMPLATE.html` / `TOPICS.md` / `setup.sh` / `publish.sh` / `tools/` 这套脚手架 | 现在什么都不用补。**首发那天**要按 [[bigcat-new-repo-onboarding]] 把六处一次登齐——尤其别再漏 `build-search.yml` 的克隆循环（complexity-science 就是在这里漏了两个月） |
| `podcast-transcripts` | 同上 | **私有数据仓，永远不该发布**：README 写明「private and must stay private」，内容是第三方节目的机器转写，仅供 podcast-deepread 写作时阅读。`gh api` 显示 `private`，无 Pages | 把它加进 `audit.py` 的 `INFRA` 集合（就是开头那一行 `INFRA = {...}`），否则每个月都会误报。**千万别给它补 hub 卡片、搜索索引或 sitemap** |

- 磁盘上共 46 个仓，脚本算出 40 个内容站，其中 38 个已上线，另外就是上面这 2 个。
- caps 守卫的书面豁免仍是 7 个：cross-ref-sync、deep-reading、deep-research、mental-models、monthly-frontier、synthesis、weekly-digest。
- 登记表里有、磁盘上没有的名字：无。

---

## 2. 可增补的合成文

脚本报了 4 篇（syn-1 / 5 / 6 / 7）。**syn-6 和 syn-7 都是误报**（原因见 §3-1），真正有活的只有 syn-1 和 syn-5。

### syn-1《熵：一个词，五个房间》—— 建议增补，2 个源页都用得上

基准日 2026-08（增补）。

#### 源页 A · `/blog-deepread/shtetl-optimized-blog6.html`（新增于 2026-09-04）· 🔴 优先

Aaronson 页里的「想法三：咖啡杯」那一节，加上紧接着的「然后他真的去做了——然后错了」。

**→ 主要补进 §8「推理在哪里停下」第一问（微观态是什么，按什么粗粒化打包？）**

第一问现在的论证是：粗粒化的方式选得不一样，答案可以差出任意倍。但给的例子是一个假想的房间。Aaronson 这里有一个**真实发生过、还公开更正过**的版本：他和 Carroll、Ouellette 做了一个咖啡自动机，把画面粗粒化后用 gzip 压缩，测出了一个「复杂度先升后降」的鼓包。论文挂出去几天，Werness 来信指出这个鼓包大概率是**粗粒化时把边界像素取整造出来的伪影**；而且按 Liggett 2009 的结果，他们选的那个模型根本产生不了大的表观复杂度。顶尖的人、正经的实验，量出来的东西也是在粗粒化这一步上造出来的。这正是第一问要说的，而且比房间那个例子硬得多。

**→ 次要补进 §5「生命：有序是借来的」末尾（一两句即可）**

Carroll 那个问题本身：熵一路单调上升，「有趣程度」却是先升后降，星系和大脑都只出现在中间这一段。这正好拿来提醒读者，「有序」和「低熵」不是一回事。Kolmogorov 复杂度在这里失效（纯随机串的 Kolmogorov 复杂度最大），才逼出了 sophistication / complextropy。另外，Aaronson 自己从这次错误里得出的结论是：要在走向平衡的路上得到复杂，**光让一堆粒子各自乱走是不够的**，得多费点劲。这和 §5 讲耗散结构的那段（必须有能量流穿过）是同一个方向，可以互相照应。

#### 源页 B · `/chapter-deepread/dbinternals-ch12-anti-entropy-and-dissemination-book130.html`（新增于 2026-09-30）

**→ 补进 §5 已有的那句括号**：「（分布式系统里有个佐证：Cassandra 和 Dynamo……anti-entropy repair。）」

这句话现在**没有深链**，而这一页刚好就是它的出处，补个深链是顺手的事。但更要紧的是**用词得改**。这一页自己说得很清楚，「反熵」这个名字取自「对抗发散」，算的是副本之间的不一致，没有微观态，也不取对数。拿 §8 那四个问题来量，它是一次**借形状**，算不上「佐证」。合适的写法是把它当成「结构是动词」的工程版：页面里那句「收敛是你雇人去做的事，不是协议的副产品」，还有「最终一致系统的健康度，等于你的反熵预算」，说的正是「断流即溃散」。另一个选择是挪到 §8「耗散结构那个类比就站得住得多」那一段，当作一次诚实的借用：它老老实实核算了流量（repair 多久跑一轮、跑不跑得完）。**不管放哪，「佐证」这两个字都该换掉**：按全文自己定的标准，这里是用词过头了。

### syn-5《注意力》—— 建议增补 2 篇，另有 2 篇可选、4 篇建议放弃

基准日 2026-08（发布）。

#### 🔴 `/blog-deepread/the-convivial-society-blog11.html`（Sacasas，新增于 2026-09-09）

**→ 补进「市场上那件商品」，放在「这句话把注意力从一种心理状态改写成了一种存量。存量能被计量，也就能被开采」之后**

这一节目前只有一个方向：西蒙把注意力定成存量，接着讲它是怎么被开采的。Sacasas 是**专门反对这个框架本身**的人，而他以前正是这个框架的拥护者。他的推论是：一旦把注意力叫作「资源」，就已经同意它可以被开采了；接受「稀缺资源」的说法，等于在替注意力经济写合法性证明（他用 Illich 的「稀缺的历史」和圈地运动来类比）。他的反命题是「你拥有的注意力恰好够用，前提是你知道此刻什么是好的」，这把问题从「怎么分配」挪到了「怎么判断」。这条正好可以接到下一站薇依那里，薇依同样不谈吞吐量。

页面里还有一个三步循环（Citton / Crary 材料，1800 年代至今）：**环境问题被转译成个人缺陷**。这和本节末尾「把停不下来归因于自控力差是错的，这是环境设计问题」是同一个判断，Sacasas 补上了历史纵深。

**→ 也可以在第四问（「它在解释，还是在给一件事涨价？」）里提一句**：「注意力是稀缺资源」本身就是一次涨价。

#### 🔴 `/deep-reading/four-thousand-weeks-read951.html`（《四千周》，新增于 2026-09-27）

**→ 补进「市场上那件商品」末段，当作和上面那条「环境设计问题」唱反调的声音**

伯克曼承认平台确实在设计成瘾，但他追问的是：为什么偷得这么容易？他的回答是，分心的引力主要来自你正要面对的那件事，因为专注会让你撞上自己的局限，「我们不是受害者，是同谋」。这和现在这一节「是环境设计问题，不是自控力问题」的结论有**真实的张力**，写进去以后这一站就不再是一边倒了。注意他没有退回「意志力差」，他的解释和自控力是两回事，写的时候要守住这条线。

**→ 次要：「还有一种注意力」那一站**。他那句「你活着的全部体验，就是你注意过的东西的总和」，和契克森米哈伊「自我是注意力投向的总和」几乎是同一句话。并列引用会显得重复，**只取上面那一处就够了**。

#### 可选（有用，但不加也不缺）

- `/chapter-deepread/gaisdi-ch11-text-to-video-generation-book103.html` → 「机器里那张表」最后一段「别让它关注全部」：分解式时空注意力的理由是一个硬数字，全 3D 注意力约 4.6 亿对、分解后约 2250 万对，**差 20 倍**。现在这一段已经有 KV cache 那组数字了，再加一个只是多一个例子。
- `/chapter-deepread/gaisdi-ch09-text-to-image-generation-book101.html` → 第五问「权重高的地方就是它在看的地方吗」：交叉注意力那张对齐表是软的、没人监督，所以「红帽子蓝围巾」会画成串色、「三只猫」会画成两只。这是一个**直接在输出里就能看到**的注意力对不上号的例子，比热图更直观。

#### 建议写进 `evaluated_rejected`（读过，只是顺带提到）

- `/deep-reading/deep-work-read949.html`：讲生产力和刻意练习，「注意力是可训练的能力」这个角度已经由 leadership/attention-energy-day67 和 mental-models/energy-attention-day27 覆盖了。
- `/chapter-deepread/gaisdi-ch03-google-translate-book95.html`：注意力在这里只是「解码器能回头看」的一句复述，Bahdanau 那篇已经讲透了。
- `/blog-deepread/nadia-xyz-blog16.html`：「维护者的成本在注意力这一侧」是一个有意思的供给侧视角，但要写就得开第五站，撑不起来。
- `/health-longevity/meditation-plan.html`：这是一份练习计划，没有论证。「练的是回来的速度」这一点已经由 psychology/curiosity-boredom-day38 覆盖了。

### syn-6《记忆》、syn-7《因果》—— 误报，无需增补

脚本报了 9 个页面，都写着「新增于 None」：psychology/trauma-body-day8、parenting/{brain-development-day3, learning-habits-day5, math-enlightenment-day6}、mental-models/scientific-method-day12、writing/memo-writing-day9、history/{modern-china-day3, wwii-day2, reform-opening-day4}。我逐个 `git log --follow` 查过，**全部是 2026-05 的老页面**（最早 05-15，最晚 05-31），远早于这两篇 2026-09 的基准日。

---

## 3. 顺带发现的异常

1. **audit.py Part B 会把改过名的页面当成新页面（这是上个月 fail-open 问题的主因）。** `git log --diff-filter=A` 默认开着改名检测，五月那次「week→day / 拼音→英文」统一改名之后，这些文件在日志里只记成 `R`（改名），不会出现 `A`（新增）。于是 `added` 里查不到它们，回退成 `'9999'`，每一篇基准日较晚的合成文都会把它们报一遍。实测有改名历史的仓，漏掉的页面数：psychology 24、parenting 24、writing 26、mental-models 17、history 8。
   **修法（一行）**：在 `part_b()` 那句 `git log` 的参数里加上 `'--no-renames'`。加上之后改名的页面会取到改名那天（2026-05 下旬），误报就消失了。顺带建议把 `added.get(p) or '9999'` 改成 fail-closed，或者至少让取不到日期的页面单独打印一行警告，别混在命中列表里。没有动手改，等 BigCat 定。
2. **syn-6、syn-7 的基准日显示成「2026-09-31」。** 这是脚本给 `YYYY-MM` 补日期时一律补 `-31` 造成的，九月没有 31 号。因为只做字符串比较，不影响结果，只是看着别扭。
3. **上期遗留的 TTS 待办状态未核实。** 上期记了 syn-3 有 5 个 R2 旧 mp3 待回收（`fce94f6546b02dca` / `d8be37b0cbf0e235` / `96283b8cd37cfd6f` / `a193f4dcba05dd59` / `2cd96f137bc6cbbb`，在 `bigcat-audio/synthesis/zh/`）。这次 session 没有 R2 凭据，没法确认是不是已经清掉了。如果还没清，这一项仍然有效。

---

## 小结

- 登记缺口 **0** 处。另有 2 个误报，处理方法：`podcast-transcripts` 加进 `INFRA`；`podcast-deepread` 首发时六处一次登齐。
- 建议增补的合成文 **2** 篇：
  - **syn-1**：Aaronson 那一页进 §8 第一问和 §5；反熵那一页给 §5 的括号补深链，并把「佐证」改掉。
  - **syn-5**：Sacasas 和伯克曼都进「市场上那件商品」。另有 2 篇可选、4 篇建议写进 `evaluated_rejected`。
- syn-6 / syn-7 是误报，根因是 audit.py 少了 `--no-renames`。
