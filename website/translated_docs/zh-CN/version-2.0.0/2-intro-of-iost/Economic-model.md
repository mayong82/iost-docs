---
id: Economic-model
title: 经济模型
sidebar_label: 经济模型
---

# 概要

目前使用最多的两个经济模型为，ETH的使用权经济模型和EOS的租赁经济模型。

IOST的贡献度经济模型致力于继承成熟经济模型的优点，避免缺点。真正实现一个免费使用、适合大规模商业DAPP落地的经济模型。

经济模型对比如下：

| 系统 | 模型 | 优点 | 缺点 |
| :---: | :----: | :----- | :----- |
| ETH | 使用权 | 1.免费创建账号<br>2.竞争使用资源，平衡网络使用率<br>3.Gas收费粒度更细，更精准  | 1.系统繁忙时，网络使用价格会非常昂贵，而且价格波动大<br>2.系统性能低，并且开发、部署和使用网络会持续收费，很难支持大规模DAPP应用<br>3.存储空间无法释放退费，用户没有动力释放存储，垃圾数据较多<br>4.CPU资源和存储资源，统一用Gas支付，导致两个资源相互影响，使用率低 |
| EOS | 租赁 | 1.拥有全网多少代币，就等量拥有全网多少资源<br>2.使用系统需要质押Token，不会消耗Token，支持大规模DAPP应用<br>3.跟系统租赁RAM，用户有动力释放空间，赎回Token，减轻区块链数据膨胀问题 | 1.创建账号复杂，收费高<br>2.大户质押Token获取资源，会导致散户资源被稀释，即使网络空闲时，散户也用不起EOS网络<br>3.需要租赁的资源种类过多（NET、CPU和RAM），普通用户操作门槛高 |
| IOST | 贡献度 | 1.创建账号简单、费用低<br>2.贡献越大，可以使用的系统资源越多<br>3.使用系统需要先质押Token获取GAS，不会消耗Token，真正的免费公链<br>4.使用Gas计价，可以有效避免EOS大户质押Token稀释散户资源，更加公平<br>5.系统资源分为CPU和存储两种，资源划分更细有利于差异化定价，避免ETH资源使用率不高问题 | 经济模型复杂度高 |


# 增发
    
IOST区块链系统初始Token总量为210亿，每年增发为2%，用于奖励超级生产者。

### 增发频率
每当有造块节点触发贡献值兑换Token奖励时，计算一次增发量，即为动态不定期增发。

每次增发量 = 年通过膨胀系数（1.98%）* 当前IOST总量 * 两次增发时间间隔（单位毫秒） / 每年总时间（单位毫秒）

年通胀系数计算公式 ：(1+x)^n = 214.2/210

由此解得 x = ln1.02 = 1.98%

x为通胀系数，n为增发次数，214.2亿为一年通胀后Token总量。

# 激励

激励模型是整个经济模型的重要组成部分，激励分两种，造块激励和抵押激励。

造块获得的贡献值可以在奖励池中兑换Token奖励。质押Token可以获得GAS，用来支付交易费用。

造块节点每造一个块最多可以获得1个贡献值，造块节点随时可以用贡献值，在奖励池中兑换Token奖励。

兑换奖励数量 = 奖励池中Token总量 * 节点的贡献值 / 全网贡献值总量 

兑换后销毁贡献值，每隔24小时可以兑换一次

### Gas奖励
    
普通节点通过质押Token可以获得Gas，1Token = 10000Gas/Day，质押的Token被锁定不能交易。

规则：

- 质押1个IOST，立刻获得10000个GAS，每天生产10000个GAS
- 生产过程平滑，Gas生产速度为 10000Gas/Token/Day
- 每个用户GAS的上限是总质押Token数的3倍，即2天充能完毕
- Gas被使用后，不足质押Token的3倍时，根据Gas生产速度，继续增加Gas
- 随时可以发起IOST赎回，申请赎回的Token不再产生GAS，赎回需要等待72小时
- 如果IOST被赎回，奖励Gas上限相应降低，超出上限的Gas被销毁。质押全部赎回时，Gas清零

### Gas使用

- 交易执行需要消耗Gas
- 交易消耗的Gas数量 =  命令的CGas（Command Gas）消耗 * 命令次数 * Gas rate
- Gas不能交易
- 每次发起交易时，先计算用户当前拥有的Gas数量，用最新的Gas余额来支付交易费用

### 邀请奖励

超级节点创建账号和邀请的用户消耗Gas时，超级节点可以获得可流通的Gas

使用:

- 流通Gas可以交易
- 可以当普通Gas使用，账号优先使用不可流通的Gas
- 持有流通Gas无需质押Token

获得:

- 超级节点每创建一个账户，会奖励30000流通Gas
- 账户可以填写邀请人，如果邀请人为超级节点，账号消耗GAS的15%，奖励给超级节点流通Gas。
- 流通Gas没有总量上限

# 资源
    
系统资源分为NET、CPU和RAM，我们将NET和CPU创新的抽象成GAS付费，RAM的使用需要质押Token。

RAM：

- 系统初始RAM上限为128G
- 用户跟系统买卖RAM，买卖RAM需要收取1%手续费。收取手续费，可以避免用户频繁操作
- 手续费会被销毁
- 系统剩余的RAM越少，价格越贵，反之越便宜
- 质押Token是为了鼓励用户释放不使用的RAM空间，赎回质押的Token
- 每年RAM增加64G，每天RAM空间增加 175.34MB
- 创建账户需要少量的RAM，避免创建账户攻击

# 流通
    
Token的流动性，反应了经济系统的繁荣程度。增加Token流动性，是经济模型设计目标之一。

IOST公链是新一代的高性能、免费公有区块链，用户免费使用系统，可以极大的促进DAPP的繁荣和C2C转账的使用。

# 回收

Token回收主要是为了平衡供需，防止通货膨胀。

- 投票、购买RAM和质押获取Gas
- 购买RAM的手续费会被销毁
- 随着使用系统人数的增加，被质押的Token也会增多，系统是通货紧缩的。
- 执行交易消耗的Gas会被销毁。