## Compound —— 别忘了你钱包中数字资产的利息！

### 概览

- 团队：6名核心成员，分布于旧金山和加利福尼亚
- 白皮书：https://compound.finance/documents/Compound.Whitepaper.v03-a457878fa6c97a53d81c275f867982f3.pdf?vsn=d
- 当前阶段：已上线测试版本
- 众筹时间：尚未公布
- 官网：https://compound.finance

### 众筹信息

* 暂无

### 社区活跃度

- Twitter 关注人数：397
- Medium 关注人数：126
- GitHub 活跃度：自2017年11月开始智能合约代码开发，至2018年3月完成大部分代码，目前测试网络已上线，近2个月内并无新的代码提交历史

------

### 需求背景

​	谈到数字资产大家一定不会陌生，小编下面提到的数字资产仅仅狭义的指ETH、BTC等加密数字货币资产。我们经常将这些数字资产同传统的金融资产做比较，再具体点说，我们将数字货币和法币相比较，但是法币有个常见且必须有的功能是目前的数字货币所不具有的，那就是利息！可能有些人会反驳说，我的XX币每天都能收到奖励呀，嗯确实，目前部分POS共识机制的币放在钱包中每天都能收到奖励（例如HSR），但这算是挖矿奖励，并不是利息，根据维基百科的定义，利息是指负债方为借债向债权人所付的补偿性费用。因此此类token收到的并不是利息，而且BTC之类的非POS系的加密货币更没有利息这一说。

![RU16q.jpg](https://s1.ax2x.com/2018/06/08/RU16q.jpg)

​	讲道理，既然是数字货币，那么应该有个地方让我储蓄并产生利息，在法币时间中这个地方是银行，然而币圈推崇的是去中心化，显然容不得这种旧世界的产物:sweat_smile:。前几天有媒体报导imtoken在过去几年里已处理了约350亿美元的存款，超过99%的美国银行。这350亿流经钱包的资产即使以3.5%左右的活期利率也能产生惊人的利息！可惜去中心化世界目前还没有这样一个所谓的“银行”，从利息角度来看现在最贴近这个目标的应该是ETHLend项目，主打去中心化的数字资产抵押借贷（本公众号曾经发布过介绍 ETHLend借贷的文章，可以回顾下），嗯~ o(*￣▽￣*)o 已经迈出一大步了，但是用过的朋友一定多少会抱怨下，真的不是太方便，由于是点对点的借贷，意味着平台上的订单是异步成交的，并且用户需要手动执行一系列操作才能借出或借入数字货币，能再方便一点就好了呢:pig:。听小编抱怨了这么多，有人一定不耐烦了，所以该轮到今天的主角登场了：对于利息这件事，**Compound**会给你整的明明白白。

​	另一方面，凡是在币圈混上个2，3个月，手里少则5，6种，多则两位数的币。有些人执意囤币（HODL），有些人则等待时机卖出。然而时不时出来个“百倍”项目ICO，大家难免会起梭哈心理，然而手头子弹（ETH）有限，真是大写的尴尬啊！

![dj8or.gif](https://s1.ax2x.com/2018/01/06/dj8or.gif)

想要梭哈唯有割肉换子弹。此时假如能够抵押手头其他货币借到弹药，然后梭哈上线后出货回本再偿还ETH，岂不完美操作！

### 项目简介

![RUIeR.jpg](https://s1.ax2x.com/2018/06/08/RUIeR.jpg)

​	根据官网的描述，Compound是一个基于以太坊的开源的金融货币市场协议，由一系列算法协调，高效透明。允许用户不通过挂单等操作便捷的赚取利息或借贷各类ERC-20代币。Compound协议内的算法能够根据不同代币的市场供求自动调节货币市场的利率。这使得用户和第三方应用可以第一次不再关心利率、复杂的借贷流程以及各种专业概念，傻瓜式的在市场上交易ERC-20代币的时间价值。想想就觉得美滋滋，一直以来，我们躺在钱包中的大量数字资产无法获得利息的时代即将终结！

### 路线图

![RCoyl.png](https://s1.ax2x.com/2018/06/08/RCoyl.png)

* 2018 Q2

  Compound Web，实现了所有Compound协议的Web应用，支持用户使用MetaMask、Mist等以太坊钱包进行数字资产的借出、借入和偿还

* 2018 Q3

  Compound iOS，一个实现了Compound协议的ERC-20钱包APP。用户在钱包中的数字资产可以随时获取利息，同时可以随时任意的发送给其他地址或者交易所

### Compound 协议

​	整个项目的核心其实就是这个Compound协议，项目方目前已上线测试网络，实现协议的所有代码也已经公布在GitHub上，比起空气项目有诚意多了。在这一节中小编将结合已发布的智能合约代码阐述协议中的关键部分。

* 货币供应

  首先我们需要明白的是Compound并不是一个点对点的借贷平台，它更像是一个银行系统，汇集所有用户存入的资产，然后再从这个资金池中借贷给资金需求方。这比P2P资金撮合更加高效，并且允许用户随时提现，而在P2P中如果借款人没有提前还款，借出方是无法提前取款的。货币供应方的资产会产生利息，用户可以随时查看。Supplier合约负责这部分功能，追踪用户存入的资产，计算利息，资金提现等。

  ![RUUTA.png](https://s1.ax2x.com/2018/06/08/RUUTA.png)

* 货币借贷

  在Compound上借入资金非常方便，借款人只需要提供抵押资产（任意一种ERC20代币），Compound会实时计算抵押物价值，然后根据一定比例（即抵押率，抵押贷款本金利息之和与抵押物估值价值之比）计算出借款人的借入额度上限，随后借款人就能在Compound上任意借款啦！借用下现在小贷公司的宣传语：随存随取！无前期，也没有所谓的手续费，借多久就还多少的利息，利率就根据市场实时浮动，没有任何黑幕。具体代码实现上，借款功能由Borrower合约实现，借款调用 marketBorrow 函数，Compound允许用户随时还款任意金额，调用 repayMarketBorrow 函数，用户将偿还本金以及借款期间产生的利息。。这里我们需要额外注意的一点是，由于抵押物的价值会随时变动，当低于系统规则的抵押率时，Compound系统会有一系列操作降低违约风险，Compound会调用 liquidateMarketBorrow 函数以略低于市场价的价格（liquidation discount）出售借款人的部分抵押资产，从而使借款人的实际抵押率能再次满足系统要求。根据项目白皮书描述，抵押物会以一定的折扣出售给套利者，这一激励方案一方面促使借款人提高抵押物价值，另一方面也能吸引套利者及时抹除借贷违约风险。而且，完全能够对接compound 抵押物出售API和交易所API，实现自动化套利，只要Compound给出的出售折扣足以覆盖套利交易成本，几乎就是稳赚不赔的买卖啊。

  ![RUKJO.png](https://s1.ax2x.com/2018/06/08/RUKJO.png)

* 资产账本

  Compound 维护了一个完整的可审计的资产账本，包含了每一笔资产交易。对于每一种数字货币，满足以下等式：Cash（现款）+ Borrow= Supply + Equity（抵押资产）

  每一笔交易会涉及到借方和贷方账本，联想下财务上的复式记账法就应该清楚了。代码中实现这个功能的主要是Ledger合约，每当用户供应或者借出资金，Ledger合约就会实时更新借方和贷方账本，同时也维护着整个系统的收支平衡表。

* 利率模型

  和ETHLend之类的P2P借贷平台不同，Compound中利率不是由借出方自定义的，而是通过协议内置的利率模型根据当前市场整体的供需情况自动计算，这也是为什么Compound的借贷效率大大高于P2P借贷平台，市场最佳利率由算法自动发现。具体的利率算法是可以由管理员修改的，下面举个简单的例子：

  我们假设数字货币a的利用率如下：

  U = Borrow / (Cash + Borrow)

  那么借入利率可能如下：

  Borrowing Interest Rate = 10% + U * 30%

  而借出利率如下：

  Supply Interest Rate = Borrowing Interest Rate * U * (1 - S)

  通过以上公式我们可以看到，当U变大时，意味着此时借款需求比较大，借入利率就会相应的增加，同时借出利率也会同比例增加。需要注意的是，借出利率的公式中有个变量S，S变量控制整个系统的收益，当S等于0是，整个系统的收入（借款人支付的利息）和支出（金主得到的利息）是平衡的，即

  Borrowing Interest Rate * Borrow = Supply Interest Rate * (Cash + Borrow)

  上面这个公式其实就是借出利率公式的等式替换（当S = 0），当S > 0时，出借方得到的利息小于借款人支出的利息，这部分利息差就是整个系统的盈利，银行系统赚的也是这个利差么！

  和利率模型相关的合约有InterestRateStorage，这个智能合约会在每一个块单元（10000个区块）中存储当时的利率水平，便于系统更快的计算出利率。此外还有个PriceOracle合约，以ETH为计价单位追踪资产价值。在借款时系统需要计算抵押物的价值，已经在借款过程中系统会实时计算抵押品价值是否低于一定阈值，系统通过这个资产价格预言机获得每种资产的价值，目前该价格预言机从TOP10交易所获取价格数据。

  ![RULf9.png](https://s1.ax2x.com/2018/06/08/RULf9.png)

### 团队

![RCq8J.png](https://s1.ax2x.com/2018/06/08/RCq8J.png)

![RE3HB.png](https://s1.ax2x.com/2018/06/08/RE3HB.png)

### 资金背景

2018年5月团队募集到了820万美金的种子轮投资。该轮由贝恩资本（传统资本巨头）、A16z（区块链投资的老玩家了，投过Ripple、Coinbase、兰花、BaseCoin、IPFS等）、Polychain Captical（参与过Dfinity、NuCypher、兰花、Coinlist等）领投，跟投方包括Transmedia Capital, Compound Ventures, Abstract Ventures, 丹华资本 和Coinbase。这里我想着重提一下Coinbase，Compound是Coinbase基金募集完成后的首批投资项目之一，我们知道Coinbase本身有做集交易、法币购买等功能于一体的数字货币钱包，并且一直在探索为加密货币用户提供优秀的体验和资产管理服务，考虑到Compound的愿景，就不难明白为何Coinbase要做这项投资。我想未来如果一款数字货币钱包能便捷的提供存款、借贷等功能，并且用户还能通过存款获得利息，谁不会心动呢，毕竟没人和钱过不去:smile:。

![RUt5e.jpg](https://s1.ax2x.com/2018/06/08/RUt5e.jpg)

------

### 优势

* 区块链目前在主要应用还是在金融市场，Compound所提供的功能精准的满足了市场需求（资产利息和借贷）。
* 相比于同类产品（ETHLend），集中式借贷效率更高，且能做到随存随取。
* Compound 核心功能开发完毕， 目前已上线测试网络
* 背后机构实力强大，有Coinbase的介入颇具想象空间

### 挑战

* Compound 可以算作是由一系列智能合约实现的银行，因此安全性至关重要，一个小小的BUG很可能会毁灭整个系统，并且会对用户资产带来巨大危害，团队需要对安全性投入200%的关注。
* 对于某些极端情况的应对能力值得考量，假设当某一种抵押物价格由于突发情况发生剧烈波动（例如由于智能合约安全漏洞导致代币价值归零）时，必定会造成抵押物价值严重不足进而导致大量抛售给套利者，如果此时购买该类资产的资金量不足是否会危机整个货币系统的稳定性。随着系统复杂性增加，这些问题都需要仔细考虑
* 目前只支持ERC-20系列代币的接待和存储，相比于其他P2P类借贷项目具有一定局限性

------

### 总结建议

​	吹了这么久，什么建议不用多说了吧。虽然官方目前没有公布任何ICO的计划事宜，但Compound是一个非常值得关注的项目，假如能参与一定毫不犹豫去撸！

------

## 更多信息敬请关注微信公众号 BlockGeeks

![d5L8y.jpg](https://s1.ax2x.com/2018/01/05/d5L8y.jpg)





