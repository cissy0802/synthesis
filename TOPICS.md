# 跨站合成 · Synthesis TOPICS

Hub 层的长文路线图。**这条线的目的是把存量变成网络,而不是继续加长列表**——不写新知识,只写「已经写过的东西之间的关系」。

**重心在共通点。**同一个结构在不同学科里被反复撞见,意味着一个领域辛苦挣来的结论(定理、下界、不可能性结论)在另一个领域可以直接提货——省掉重新发明的成本,这是跨学科互联值得做的全部理由。**边界也要写,但它服务于共通点**:正因为提到手的是真东西,才需要知道它在哪里就不跟着走了。反过来写成通篇挑错,这条线就跑偏了。

## 这是什么

普通内容站回答「X 是什么」;合成文回答「**X 这个东西,在我这几个站里分别是什么,以及它们为什么对不上**」。每篇的源材料**全部来自本 hub 已发布的页面**,每一节都深链回源页——读者可以顺着链接钻回去,存量因此变成一张网。

## 选题标准(硬门槛)

一个概念**跨站出现**不构成选题理由。必须同时满足:

1. **甜区 4–8 站**。覆盖 15+ 站的概念(如「风险」18 站、「决策」21 站)写出来必然是浆糊——每站沾一句,哪站都不深。少于 4 站则不成网。
2. **各站背后的推理真正不同**。同一个词在各领域底下压着不同的机制,而不是同一件事换个说法。(早期版本这里写「机器」,是内部速记,已弃用——正文里别用这个词,直接说「机制」或点名具体内容:定理、下界、不可能性结论。)
3. **有一个锋利的钩子**——通常是下面两种之一:
   - **共通点 + 边界**:几个领域底下是同一套推理,而这套推理在某处不再跟着走(如熵:四个领域算的是同一个数,「房间会变乱」借走的只是词的形状)
   - **透镜差**:同一对象被几个学科看见了不同的层
   无论哪种,先讲清**为什么这个联系是真的、它换来了什么**,再讲边界。
4. **源材料实打实**:至少 3 个站有**成篇**(而非顺带提及)的源页。

**反面教材**:凑数式的「这个词在 12 个站出现过」;把收敛写得太便宜(如「科学证实了佛陀」);没有边界的平铺罗列;以及反过来——通篇在挑别人用错了,却没讲清这个联系本身值多少钱。

## 三种体裁

- **A. 同一个词,不同推理** —— 词旅行到别的领域,底下那套推理未必跟过来。先写清**跟过来的部分为什么是真的、换来了什么**,再写清**没跟过来的部分停在哪**。
- **B. 同一个对象,多重透镜** —— 一件事被几个学科各看到一层。灵魂是**透镜之间的互补与冲突**。
- **C. 同一套方法,跨域复用** —— 一种推理工具在各领域的不同要求与标准。

## 约定

- 文件名 `{slug}.html` + `{slug}.en.html`,放本仓根目录(线上是 `hub.cissychen.com/synthesis/{slug}.html`)
- **中英双语,手写独立页,无自动同步机制——改一版必须同时镜像另一版**(含 SVG 标签翻译)
- 页尾脚本硬写(本仓不在共享 JS 注入 Action 的覆盖范围内,与 deep-research 同样处理):
  `<script src="https://hub.cissychen.com/comments.js" defer></script>` 和 `search.js`
- 返回 hub 的链接用**根相对且语言正确**:中文页 `/index.zh.html`、英文页 `/index.en.html`
  (⚠️ 别用 `index.html` —— 它是英文默认的跳转 stub,中文页链它会把读者弹去英文版)
- **篇幅 4500–6000 中文字。各领域的介绍要短——只留后面论证真正用得到的,其余交给深链。**源页已经把每个领域讲透了,合成文再讲一遍,深链就成了摆设
- 每篇写完:① 把引用的源页路径登记进 `synthesis-map.json`(供反向链接注入);② 把新文章加进 `index.html` 与 `index.en.html` 两个落地页,否则成孤儿页
- 搜索索引自动覆盖:本仓已在 hub 的 `build-search.yml` clone 循环里,无需另行登记
- hub 首页的卡片入口在 `generate_hub.py` 的 `SYNTHESIS_CARDS`,是**整个站一张卡**,加新文章不用动它

**为什么独立成仓**(2026-07,写完 Syn 1 后迁出):原计划放 hub 仓根目录,实操下来发现 hub 根目录的手写长文落在所有自动化路径之外——导航链接槽、sitemap、搜索索引三处都得手工补,而且 `blog-pipeline` 因此**从来没有被搜索索引过**。分界线是:**一次性的东西留在 hub 根目录(blog-pipeline),成系列的东西开仓。**
- **由本地 routine 周更生成**(`~/.claude/scheduled-tasks/weekly-synthesis/SKILL.md`,每周四 09:00 本地时间,与 `weekly-deep-research` 同一套机制)。**改写作规则改那份 SKILL.md**
  (原计划「暂不做 routine、先手写 3–4 篇」已于 2026-07 推翻:Syn 1 手写完即开 routine)
- **必须本地跑,不能改成云端 routine**:云端沙箱访问 `hub.cissychen.com` 整站 403、`api.github.com` 也被挡,读不到线上页面;本地才能直接读 `~/Desktop/repos/` 下的源仓,而「真读了源页」是这条内容线成立的前提
- **routine 不许自己发明选题**:只能挑本文件里编号最小、且还没写的一条;写完全部条目就停下发 PushNotification 请求补充,**绝不自造主题**
- **routine 不许改本文件**。新条目由 BigCat 补充
- **合成文是活的**:源站继续更新时,已发布的合成文可以增补新的一节(如 physics 补上拓扑物态后,Syn 17 才补齐)

---

## 已发布

### Syn 1. 熵:五个房间里的同一个数 〔A〕 ✅ 2026-07
- 页面:`entropy.html` × zh/en · <https://hub.cissychen.com/synthesis/entropy.html>
- 共通点:四个领域(热力学 / 信息论 / 机器学习 / 生物能量学)算的是**同一个数**——微观态等可能时 `S=k log W` 与 `H=−Σp log p` 只差换算常数 k。四者问的是同一个问题:「在我能看见的之下,还有多少种可能」,而数学不问这些可能性是什么做的。
- 承重证据:兰道尔原理(擦除 1 比特 ≥ kT ln2 的热)给了比特与焦耳一个汇率,并据此解决了卡了七十多年的麦克斯韦妖悖论——判据是「它解决过一个原本无解的具体问题」,而不只是让人觉得优雅。
- 互联换来了什么:信息论拿到压缩的地板(编码定理);机器学习拿到有物理意义的损失函数(loss 的单位是比特/token);生物学摆脱「生命是否违反第二定律」的困惑(开放系统的账可以真算)。
- 边界判据(四问):① 微观态是什么、按什么粗粒化打包?② 有单位吗、能报出两个时刻的值吗?③ 那条定律是从大数(10²³)里涌现的吗?④ 是不是把开放系统当成了孤立系统?——四问全过是测量,机制说得清是模型,都不过是修辞。
- 源页:10 篇 / 6 站 —— `physics/entropy-arrow-day7`、`heat-temperature-day6` · `mathematics/information-theory-day13` · `ai-ml/loss-optimization-day10`、`probability-information-day33` · `meta-knowledge/bioenergetics-day23` · `deep-reading/order-of-time-read18`、`flow-read15` · `mental-models/information-theory-day58`、`physics-thinking-day36`
- 未用上的备选源:`book-recommendations/time-many-faces-book29`(时间的多副面孔)——写时觉得与 Read 18 重合过多,留给日后增补
- 后记:初稿把重心压在断裂点上,读起来像挑错;2026-07 重写为「先讲共通点与它换来了什么,边界服务于共通点」。这条经验已写进本文件的选题标准与 `weekly-synthesis` 的 SKILL.md。

### Syn 2. 进化博弈:同一副底牌,三种文明 〔B〕 ✅ 2026-07
- 页面:`evolutionary-game.html` × zh/en · <https://hub.cissychen.com/synthesis/evolutionary-game.html>
- 共通点:进化给所有人类社会发了**同一副底牌**——亲缘利他(汉密尔顿 `rB>C`)、互惠利他、以牙还牙、群体边界;差别在于不同环境把不同的牌推到主位。三种文明回答的是同一道题:「如何让一群携带自私基因的灵长类合作」。
- 承重:差序格局=亲缘利他制度化(费孝通的涟漪≈Hamilton 公式的社会学翻译);契约/法治=让 tit-for-tat 在陌生人社会运转的基础设施;种姓=固化群体边界降低搜寻成本;而各自的哲学是给已运行的操作系统写说明书。价值在翻译——一个文明的制度创新可被另一个直接提货。
- 边界(三条):① 进化博弈解释约束不解释选择(宋代有一切物质前提却没走向工业革命);② 文化传播是水平的、比基因遗传快几个数量级,速度常数变了;③「同一道题」只抓底层,每种文明的上层建筑远比底层丰富。
- 源页:9 篇 / 6 站 —— `deep-reading/selfish-gene-read2`、`from-the-soil-read21`、`guns-germs-steel-read4` · `mental-models/game-cooperation-day28`、`ecology-evolution-day18` · `psychology/evolutionary-psychology-day32` · `philosophy/indian-darshanas-day33` · `thinker-arena` 圆桌:`geography-shapes-thought`、`east-west-philosophy`
- 与原路线图的关系:本篇不在原 17 篇清单内;写作后占用 Syn 2,原「合作的演化」顺延为 Syn 3,其后各篇依次 +1。

## 第一梯队(材料厚 + 钩子锋利)

- **Syn 3: 合作的演化** 〔A/C〕— 「为什么会有合作?」四套**互不相容**的答案:演化生物学算基因的账(汉密尔顿 `rB>C`)、博弈论算重复的账(Axelrod 的 tit-for-tat)、国际关系算可信承诺的账、佛学**拒绝算账**(菩萨道不图回报)。前三套用「其实是自利」消解利他,第四套掀桌子。收尾落在自然主义谬误。
  源:`mental-models/game-cooperation-day28`(博弈 60 / 合作 21)、`strategy-day04`、`evolutionary-psychology-day53` · `meta-knowledge/game-theory-day11`(40)、`trust-cooperation-day58`(26)、`evolutionary-biology-day4` · `deep-reading/selfish-gene-read2`(合作 28 / 选择层级 15) · `civics-geopolitics/war-and-peace-rules-day13`(可信承诺 13)、`great-power-rivalry-day10` · `buddhism/bodhisattva-day11`(利他 21) · `leadership/office-politics-day6`(19) · `philosophy/individual-society-day15`、`ethics-virtue-day5` · `psychology/evolutionary-psychology-day32` · `sales/trust-currency-day2`(信任作为昂贵信号)
  待补:book-recommendations Issue 62《博弈论与合作的演化》发布后再加一节书单锚点

- **Syn 4: 自我,与无我** 〔B〕— 全站最惊人的一次东西方收敛:佛学两千年前说「无我」,神经科学从**注意图式理论**走到几乎同一结论——自我是大脑造的一个模型、一个有用的失真。**但别让收敛太便宜**:佛学的无我是修行结论(看破我执为离苦),神经科学的自我模型是价值中立的机制描述;把 AST 当成「科学证实了佛陀」是廉价的胜利。收尾落在意识难题——两条路都没解决「为什么会有主观体验」。
  源:`buddhism/dialogue-day31`(无我 35)、`lankavatara-day17`、`yogacara-day3`、`mysticism-day36` · `neuroscience/self-model-topic12`(注意图式)、`global-workspace-topic13`、`hard-problem-topic10`、`neural-correlates-topic11` · `philosophy/free-will-day3`(无我 16)、`life-death-day6`(人格同一性)、`consciousness-awareness-day25`、`existence-day1` · `psychology/consciousness-day24` · `book-recommendations/mind-machine-book9` · `deep-reading/being-you-read20`
  已知缺腿:**AI 那条**(「LLM 有没有自我」)几乎无材料,仅 `cs-papers-deepread/constitutional-ai-paper15` 沾边

- **Syn 5: 注意力** 〔A〕— 词从心理学 → 机器学习 → 经济学**旅行了三轮**,三套机制毫无关系:Transformer 的 QK 点积、丘脑的选择性门控、作为稀缺资源被交易的注意力。
  源:`ai-ml`(8 页,注意力机制) · `neuroscience/attention-topic2` · `super-individual`(5 页,注意力经济) · `cs-papers-deepread`(2 页) · `mental-models` · `philosophy`(专注)

- **Syn 6: 记忆** 〔A/B〕— 「模型记忆」和「人的记忆」是不是同一回事?LLM 的 context window ≠ 记忆,参数里的也不是——这个混淆在产品设计上代价很大。
  源:`neuroscience/long-term-memory-topic4`、`working-memory-topic3` · `ai-ml`(8 页) · `meta-knowledge`(间隔重复) · `mental-models`(6 页) · `super-individual`(6 页,agent 记忆工程) · `book-recommendations`(7 页)

- **Syn 7: 因果** 〔C〕— 史学家、流行病学家、ML 工程师说「因果」时,**要求的证据标准差三个数量级**。
  源:`history`(23 页,史学因果) · `health-longevity`(混杂与 RCT) · `ai-ml`(相关≠因果) · `meta-knowledge`(Pearl 因果阶梯) · `mathematics`
  待补:meta-knowledge Day 67「因果推断」发布后作为主锚

## 第二梯队(成立,材料够)

- **Syn 8: 复利** 〔A〕— 断裂:金融复利有**再投资**这个物理机制;「技能复利」「人脉复利」只是激励隐喻,没有对应机制。
  源:`investing`(17 页) · `personal-finance` · `leadership` · `writing` · `mental-models`

- **Syn 9: 睡眠** 〔B〕— B 类范本:同一件事的生理 / 认知 / 发育 / 行为四层透镜。
  源:`health-longevity`(21 页,含 `sleep-day3`) · `neuroscience`(记忆巩固) · `psychology` · `parenting` · `mental-models`

- **Syn 10: 死亡与有限性** 〔B〕— 科学延长它、佛学接受它、哲学追问它——三种回应同一个事实。
  源:`health-longevity`(衰老生物学 5 页) · `buddhism`(无常) · `philosophy/life-death-day6` · `deep-reading` · `book-recommendations`

- **Syn 11: 苦 / 疼痛** 〔B〕— 「苦」(dukkha)和「pain」在翻译层就不是一回事:一个是生理信号,一个是存在论判断。
  源:`buddhism`(11 页,苦谛) · `health-longevity`(疼痛生理) · `psychology`(慢性痛与情绪) · `philosophy` · `mental-models` · `deep-reading`

- **Syn 12: 幂律与长尾** 〔A〕— 断裂:大量被声称的「幂律」其实是对数正态,**误判会毁掉风险模型**。
  源:`mental-models`(6 页) · `ai-ml`(scaling law) · `investing`(尾部风险) · `cs-papers-deepread` · `mathematics` · `meta-knowledge`

- **Syn 13: 叙事** 〔B〕— 同一个工具:被用来写作、被用来构建自我、被用来给公司定价。
  源:`writing`(22 页,技艺) · `book-recommendations`(16 页) · `investing`(故事驱动估值 9 页) · `psychology`(叙事身份) · `biographies` · `art-aesthetics`

## 第三梯队(成立但更窄,或需等材料长出来)

- **Syn 14: 免疫** 〔A〕— 「认知免疫 / 思想接种」这个借喻,借得有多准确?生物免疫有记忆细胞和特异性,认知接种有对应物吗?
  源:`health-longevity`(6 页) · `meta-knowledge`(6 页,接种理论) · `psychology` · `deep-reading`

- **Syn 15: 情绪** 〔B〕— 建构论(情绪是被造出来的)vs 基本情绪论,以及审美情绪为何被排除在心理学之外。
  源:`psychology`(25 页) · `neuroscience/emotion-construction-topic8` · `parenting`(19 页) · `art-aesthetics`(18 页) · `leadership`

- **Syn 16: 临界与相变** 〔A〕— 材料最多(14 站)但**必须收窄**,否则写散。锁定四条腿即可:物理相变 / 历史革命 / 系统过载崩溃 / 疾病阈值。
  源:`physics` · `history` · `system-design` · `health-longevity` · `mental-models`(tipping point)

- **Syn 17: 拓扑** 〔A〕— 亮点:`neuroscience` 的**视网膜拓扑映射(retinotopy)是拓扑的字面实现**——大脑真的在跑连续映射;而 `system-design` 的「网络拓扑」是完美的断裂案例:词旅行了,「连续形变下的不变量」那套推理一点没跟过来。
  源:`mathematics/topology-day9`(26)、`graph-theory-day8` · `meta-knowledge/topology-day62`(48) · `mental-models/mathematical-structures-day67` · `neuroscience/ref-visual-pathway` · `system-design/cdn-edge-day28`
  **等材料**:physics 的拓扑物态(2016 诺奖那条线)尚未写,最硬的一条腿现在缺席。建议 physics TOPICS 补一行后再动笔
  **顺带发现**:`mathematics/topology-day9` 与 `meta-knowledge/topology-day62` 角度高度重合(都是「拓扑直觉科普」)——cross-ref-sync 只防 ai-ml↔super-individual,没人防这一对

- **Syn 18: 自由意志** 〔B〕— 甜区但材料偏薄(6 站/9 页)。与 Syn 4 有重叠(`philosophy/free-will-day3` 两边都用),写时需明确分工:Syn 4 问「谁在做决定」,本篇问「这个决定是不是自由的」。
  源:`physics`(决定论) · `philosophy/free-will-day3` · `neuroscience` · `deep-reading` · `super-individual`

---

## 已评估但不收录(记下来免得重复讨论)

- **信任与合作** —— 与 Syn 3 重叠过多(`meta-knowledge/trust-cooperation-day58` 是两者共同主锚),已并入 Syn 3
- **风险 / 不确定性**(18 站)、**决策**(21 站)、**稀缺**(12 站) —— 覆盖太广,不满足甜区门槛,写出来必然是浆糊
- **涌现**(10 站)、**贝叶斯**(11 站)、**非线性 / 混沌**(10 站) —— 略超甜区,若日后收窄到 4–6 条腿可重新考虑
- **美 / 审美**(5 站/9 页)、**群体与集体**(8 站/16 页) —— 甜区但材料偏薄,待存量增长
- **学习 / 技能**、**记忆巩固**单列 —— 已被 Syn 6 覆盖

## 扫描方法备忘(下次找选题时复用)

用关键词跨全站扫**已发布 HTML**(不是 TOPICS.md——路线图里的条目还没页面可链),按「站数 × 成篇页数」定位甜区。两个踩过的坑:

1. **必须剥 HTML 标签再统计**。否则 `<body>` 会让「身体」跨 22 站、`lang=` 属性会让「语言」跨 19 站、CSS 里的 `space` 会让「空间」跨 18 站——全是假阳性。
2. **短的英文缩写不能直接当关键词**。`ESS`(演化稳定策略)小写后匹配到 proc**ess** / l**ess** / addr**ess**,一次扫出 370 页垃圾。
3. **中文常用词要分维度**。「自我」在心理学站大量出现,但绝大多数是「自我效能 / 自我调节」,和「自我作为一个实体是否存在」无关——按维度分开扫才看得出真实材料。
