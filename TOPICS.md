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

### Syn 3. 合作:三本账,和一张掀翻的桌子 〔A/C〕 ✅ 2026-07
- 页面:`cooperation.html` × zh/en · <https://hub.cissychen.com/synthesis/cooperation.html>
- 共通点:三本账(基因 / 重复 / 可信承诺)其实是**同一本**。剥掉外壳全是同一张囚徒困境收益矩阵;破局装置是同一个形状——把背叛的短期收益,换算成一笔越过未来的长期代价,只是换算的钩子不同:生物学用亲缘度 `r`、博弈论用再相遇概率 `w`、国际关系用可信承诺。`r`/`w`/承诺是同一变量在三种货币里的三副面孔,都在回答「背叛的账,多久之后、以什么形式回到你头上」。
- 承重证据:汉密尔顿规则化解了达尔文自己那道「差点掀翻整套进化论」的裂痕——肯吃亏的行为(不育工蜂)为何没被斩草除根(亲缘度把利他的收益顺着共享基因导回给「未来自己」的拷贝)。判据同 Syn 1:解决一个原本无解的具体问题,而非仅仅优雅。同一副骨架还精确预言合作**怎么死**:群体过大、未来缩短、信息变噪、惩罚缺位,任一越过临界即相变式雪崩。
- 互联换来了什么:一个领域证过的定理换个房间不必重证——`w` 被 BitTorrent 写进协议(tit-for-tat 硬编码压搭便车)、`q>c/b` 被 Uber/Airbnb 双向评分工程化、区块链质押罚没把匿名节点拉进重复博弈、霍布斯那一步长成机制设计整个学科(次价拍卖让如实出价成占优策略)。
- 断裂点(五问判据):① 用哪种货币算账?(收益回流到基因 / 未来的你 / 第三方声誉——三种不能混记)② 有没有「未来的影子」?(短 → 理论预言背叛,别指望道德补缺)③ 需不需要一个有边界的「自我」做受益人?(需要 → 在算账;以消解自我为前提 → 掀了桌子,别硬塞「其实是自利」)④ 翻译成「其实是划算的自利」,原命题会不会塌?(不塌 = 本就是自利账;塌了 = 你在用廉价收敛偷走它)⑤ 讲「是」还是「应该」?(从 `rB>C` 推「所以应偏袒亲属」缺一步价值前提 = 自然主义谬误)。
- 源页:15 篇 / 9 站 —— `mental-models/game-cooperation-day28`、`strategy-day04`、`evolutionary-psychology-day53` · `meta-knowledge/game-theory-day11`、`trust-cooperation-day58`、`evolutionary-biology-day4` · `deep-reading/selfish-gene-read2` · `civics-geopolitics/war-and-peace-rules-day13`、`great-power-rivalry-day10` · `buddhism/bodhisattva-day11` · `leadership/office-politics-day6` · `philosophy/individual-society-day15`、`ethics-virtue-day5` · `psychology/evolutionary-psychology-day32` · `sales/trust-currency-day2`
- 待补:book-recommendations Issue 62《博弈论与合作的演化》发布后再加一节书单锚点。
- 后记:本题被两次 routine 撞车并发生成;先落地的版本(15 源 / 9 站,〔A/C〕)已发布,后一版(8 源 / 6 站)撞车后主动作废、未污染线上。登记步骤由后一版补全。

### Syn 4. 自我:一只橡皮手,和一个两千五百年前的论证 〔B〕 ✅ 2026-08
- 页面:`self.html` × zh/en · <https://hub.cissychen.com/synthesis/self.html>
- 共通点:两条方法上毫无交集的路,对「我」做了**同一个动作**——把它从主语挪到宾语。佛学:第七识末那**恒执**阿赖耶为我,「恒执」是个动作不是一个东西,所以「我」的实感不是某个部件发出来的,是一个持续在跑的误认动作的产物。神经科学:控制论的内部模型原理(调节器要压住某系统就必须含有它的模型)→ 大脑要调度注意就必须给注意建模 → 注意图式**故意失真**(省掉突触竞争、增益调节这些机械细节),读这张糊涂草图读出的就是「我有一份主观体验」;赛斯把同一台预测机器转向内部,「你」也是被猜出来的对象,不是在猜的主体。
- 承重证据:**主宰义论证与橡皮手错觉是同一条推理的两次实例化**。《无我相经》「若色有我者……亦不得于色欲令如是、不令如是」走的是日常观察(病、老、想让它怎样却做不到);橡皮手走的是可控干预(两把刷子五十秒改写「这只手是我的」,这个判定不归你管)。它解决的具体问题是「自我是一块还是一堆」——从两千年只能靠内省和辩论,变成可以在实验室里逐层判决:赛斯五层(身体 / 视角 / 意志 / 叙事 / 社会)每一层都能被单独撕开,而神经科学至今没找到「自我中枢」,按这套图景本来也不该有。
- 互联换来了什么:① 神经科学拿到的不是一个想法,是**一批被试和一套现成的规程**(《大念处经》四念处、《瑜伽师地论》九住心)——Brewer 2011「资深禅修者 DMN 显著降低且能实时下调」这个实验能做出来,前提是有人真在跑这套花两千年调出来的方法;② 主宰义论证可以直接从经文里拆出来当工具,松动「我是个焦虑的人」这类固化标签,而且判据本身价值中立、不要求先接受任何形而上学立场;③ AST 长成可写进工程规格的东西(给机器装注意图式),高阶理论对应元认知与校准(线性探针去读模型内部那个「我可能不确定」的信号)。
- 边界判据(五问):① 说的是哪一层?(橡皮手对身体自我是硬的;DMN 对叙事自我只是相关性证据;意志自我牵扯 Libet 准备电位与 Schurger 再分析的争议)② 是描述还是处方?(「自我是建构」不蕴含「看破我执可离苦」,中间缺一步价值前提)③ 相关还是等同?(把「DMN 变淡」等同「证悟无我」是拿神经关联物冒充解脱体验——风景的照片不是抵达)④ 这份报告能否被独立于报告地验证?(无报告范式让前额叶那片「意识信号」缩水一大截;而**同一种静默,在维摩诘的一默与商羯罗的梵我一如里被报告成了相反的结论**——卡茨建构论:没有未经诠释的纯经验)⑤ 它解释了体验,还是把体验取消了?(AST 严格说只解释「大脑为何一口咬定自己有体验」,滑向幻觉论 = 换题;唯识、大圆满反向把觉知的明知性当成不可再拆的一层——两条路在同一堵墙前停下,停法相反)。
- 分档:能被单独撕开、能报出两个条件下的差 → 测量(身体自我、视角自我);机制说得清、有可检验预言 → 模型(注意图式的颞顶交界预言;末那识作为「持续执取」的结构说明,是修行认识论而非神经学假说);既报不出数、也不打算做一个命题 → 修辞(维摩一默本就不打算成为可检验命题,出问题的只是把它搬到「所以科学证明了」那一栏)。收尾:两条路都拒绝「反正没有我,不必负责」(二谛的假名我;赛斯的相容论保住自愿行动)。
- 源页:15 篇 / 6 站 —— `buddhism/dialogue-day31`、`yogacara-day3`、`lankavatara-day17`、`mysticism-day36` · `neuroscience/self-model-topic12`、`hard-problem-topic10`、`neural-correlates-topic11`、`global-workspace-topic13` · `philosophy/free-will-day3`、`life-death-day6`、`consciousness-awareness-day25`、`existence-day1` · `psychology/consciousness-day24` · `deep-reading/being-you-read20` · `book-recommendations/mind-machine-book9`
- 已知缺腿(写作时复核仍成立):AI 那条(「LLM 有没有自我」)无成篇材料,本篇只借 `self-model-topic12` 的「AI 对读」在第四节带过;日后 cs-papers-deepread 长出来可增补一节。
- 反模仿:前三篇的结构指纹是「一个源站一节 + 编号标题 + 收尾『怎么用它』」。本篇改按**自我的分层**组织,一节里横跨多站,七节且标题不编号。

### Syn 5. 注意力:一个借错的比喻,和它换来的九个 BLEU 〔A〕 ✅ 2026-08
- 页面:`attention.html` × zh/en · <https://hub.cissychen.com/synthesis/attention.html>
- 共通点:四处用法共有的**不是机制,是一个约束的形状**——① 一条有硬上限的通道 ② 一个远大于上限的候选集 ③ 一条必须当场做出的分配决定,三个部件缺一不可。大脑:上限是下游深加工带宽(能量逼出来的)／候选集是全部感官信息／靠偏向竞争加丘脑网状核那道闸;Transformer:上限是平方级增长的算力与显存(70B 模型 8k 序列的 KV cache 约 21.5 GB)／候选集是上下文全部 token／靠 QK 点积加 softmax;市场:上限是一天醒着的时间(人·秒,能真报数)／候选集是近乎无限的内容／靠出价,广告拍卖在给它定价;薇依与心流:上限是一生能投出去的专注总量／分配决定的是「你成为谁」。约束能过关而机制不能,因为**约束不问被约束的东西是什么做的**。
- 承重证据:**巴赫达瑙 2014**。他借的不是「大脑怎么做注意」(借不到,也没人给得出),是「面对一个装不下的通道,人是怎么办的」——不背、摊着、用到哪儿看到哪儿。原问题是固定长度向量那座独木桥,而主流判断「网络不够大」是在往错方向使劲;换成按需回看后 BLEU 17.82 → 26.75,句长曲线从「20 词后下坠」变成「50 词几乎不掉」,无生僻词子集 36.15 越过统治二十年的 Moses 35.63,而对齐没有人教、是学翻译的副产品。反向佐证:Transformer 的 O(n²) 开销逼出稀疏化——**人工系统被算力逼着,重新推出了大脑被能量逼出来的同一条结论**,两边谁也没抄谁。
- 互联换来了什么:① 机器学习拿到一条不必自证的路线(GQA 把 KV cache 21.5 → 2.7 GB、滑动窗口、FlashAttention 只改搬运顺序,是同一句话的不同答法);② 管理拿到一个能报出口的约束(西蒙 1971「信息的富足制造了注意力的贫困」→ 三个判断槽位、第四件进来必须有一件出去;关键是把**判断量**和执行量分开记账);③ 心理学把责任放对地方(变量比率强化本就为抗消退设计,可动的不是意志力而是奖赏可预测性与停止点;「意志力耗竭」模型未获多实验室复制支持);④ 注意力残留(Leroy 2009):怎么**结束**一个任务,比怎么开始下一个更影响产出质量。
- 边界判据(五问):① **这道闸是硬的还是软的?**(最锋利一条:丘脑真掐断,没赢的信息从未抵达;softmax 是软加权,什么都没被扔掉、只是权重小,残余权重会跨几十层累积。所以「模型注意力权重低＝没看见」错,「够努力就能注意到」也错。但要**问系统不问物种**——上了滑动窗口或稀疏注意力,机器那边就真有硬门控了)② 这个数有单位吗、谁在报?(GB／人·秒／解锁次数能报;「深度工作能力」「三个槽位」报不出刻度——能报数的才能被 RCT 打脸,如 Allcott 2020 近三千人四周随机停用,幸福感提升只相当于心理治疗效应的一小部分)③「注意力」指的是哪一样?(波斯纳三网络各自能损坏、各自能训练;ADHD 不是缺乏注意力而是调节与抑制的发育差异,「他打游戏能专心所以是装的」恰好踩反这条;机器这边多头也不是单数,大量冗余头剪掉不掉效果)④ 它在解释,还是在给一件事涨价?(薇依是诚实借用——借稀缺性、明说要拿去干什么,不假装测量;要防的是拿一边的权威去给另一边的价值主张背书。同一把尺子也量它自己:「带来心流」≠「值得做」;薇依的怀疑武器一对准自己的出身就失去校准)⑤ 权重高的地方就是它在看的地方吗?(唯一仍有正式争论的一条:α 权重常发散、不总落在「正确」的词上,「attention is not explanation」之争由此而来。人这边的对应版本在 Leroy 实验里——受试者主观确信已全神贯注,资源却还锁在旧任务上。两边都得靠外部证据,不能靠自陈)
- 分档:报得出数 → 测量(GB、算力占比、日活时长、RCT 效应量);三部件说得清但无刻度、且给得出可推翻的预言 → 模型(注意力残留是范本;自测是「能否翻译成不含『注意力』三字的句子而不损失内容」);只在给一件事涨价 → 修辞(而修辞不是罪名,出问题的是把它搬到「所以科学证明了」那一栏)
- 源页:12 篇 / 10 站 —— `cs-papers-deepread/bahdanau-attention-paper9`、`attention-is-all-you-need-paper1` · `neuroscience/attention-topic2` · `ai-ml/attention-variants-day12` · `psychology/digital-age-day56`、`curiosity-boredom-day38` · `book-recommendations/attention-tech-critique-book35` · `biographies/weil-day49` · `deep-reading/flow-read15` · `leadership/attention-energy-day67` · `mental-models/energy-attention-day27` · `parenting/attention-adhd-day17`
- 与原路线图的偏差:原条目写的是「心理学 → ML → 经济学三轮旅行」,源站清点后发现 `super-individual` 并无注意力经济的成篇材料(那 5 页是 agent 工程,不是注意力),这条腿改由 `psychology/digital-age-day56` + `book-recommendations/attention-tech-critique-book35` 承担;`philosophy`(专注)同样无成篇材料,改用 `biographies/weil-day49` 作第四条腿,反而拿到了更硬的东西——薇依把注意力接到伦理上,是「诚实借用」的范本。
- 未用上的备选源:`psychology/self-control-day58`、`willpower-day29`(自控与意志力,与「可动的不是意志力」那条重合但更偏干预方法);`ai-ml/graph-ml-day37`、`frontier-architectures-day34`(注意力在图与前沿架构里的变体);`deep-reading/amusing-ourselves-read25`(波兹曼「媒介即隐喻」,本篇只经由 Book 35 间接带到)。
- 反模仿:Syn 1–3 是「一个源站一节 + 编号标题」,Syn 4 是「按自我的分层组织、七节不编号」。本篇按**词的旅行路线**组织(四站 + 共通点 + 收益 + 五问 + 三档),九节不编号,并首次用两张 SVG——一张画共通的约束形状,一张画硬门控 vs 软加权这条最锋利的判据。

## 第一梯队(材料厚 + 钩子锋利)

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
