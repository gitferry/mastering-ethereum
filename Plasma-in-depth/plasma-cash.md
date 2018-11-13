## 深入理解Plasma（四）Plasma Cash

> 这一系列文章将围绕以太坊的二层扩容框架 Plasma，介绍其基本运行原理，具体操作细节，安全性讨论以及未来研究方向等。本篇文章主要介绍在 Plasma 框架下的项目 Plasma Cash。

在[上一篇](https://github.com/gitferry/mastering-ethereum/blob/master/Plasma-in-depth/plasma-mvp.md)文章中我们已经理解了 Plasma 的最小实现 Plasma MVP 如何使用 UTXO 模型实现 Plasma 链下扩容的核心思想。但由于 Plasma MVP 本身过于简单，并不能用于实际的生产环境中。2018 年 3 月，在巴黎举行的以太坊开发者大会上，Vitalik 发布了 Plasma Cash 模型[[1]](https://ethresear.ch/t/plasma-cash-plasma-with-much-less-per-user-data-checking/1298)。Plasma Cash 与 Plasma MVP 的主要区别是每次存款操作都会产生一个唯一的 coin ID 对应转移到侧链上的资产，并使用一种称为稀疏梅克尔树（Sparse Merkle Tree）的数据结构存储交易历史。由此带来的好处是用户不需要关注子链上的每个动态，只需要关注跟自己的 token 有关的动态。在下文中将介绍具体细节。

### 存款（Deposits）
Plasma Cash 中的每次存款操作都会对应产生一个 NFT（non-fungible token）[[2]](https://en.wikipedia.org/wiki/Non-fungible_token)。NFT 可以简单理解为“不可互换的 token”，即每个 token 都是独一无二的，由唯一的 ID 标记。以太坊官方为 NFT 提供了 ERC721 标准[[3]](http://erc721.org/)，在之前火爆到阻塞以太坊的 CryptoKitties 就是由 ERC721 合约实现的。

在 Plasma Cash 中，当用户向 Plasma 合约发送存款交易时，合约会生成一个与存款等值的 token，并给这个 token 分配一个唯一的 ID。假如一个用户分别执行两次存款操作，而且每次存款都是 5 ETH，那么他将得到相等价值的两个完全不同的 token。和 Plasma MVP 一样，每次存款操作都会使得 Plasma 合约产生一个只包含这个存款交易的区块。

### Plasma Cash 区块

Plasma Cash 中的每个 token 都被分配唯一的 ID，因此可以按 ID 的顺序存储每个 token 的交易历史。Plasma Cash 的区块按 token ID 的顺序给每个 token 分配了一个插槽（slot），每个插槽会记录这个 token 是否被交易的信息。例如在下图(来源[[4]](https://github.com/ethsociety/learn-plasma))的区块中，包含 4 个 token，id 分别是 #1，#2，#3，#4。其中 #1，#2，#3 被标记为没有被花费，而 #4 由用户 A 发送给用户 B。

<img src="./images/pc-block.png"  width="500" height="160" alt="Plasma Cash Block" />

从上面这个例子中我们可以看到，每个插槽记录了其所对应的 token 在当前区块中的交易状态，所有存储了某个 token 的交易状态的区块按时间顺序连在一起就构成了这个 token 的全部交易历史。每当一个 token 被分配了一个 id，之后的所有交易状态都会被保存在每个区块相同的插槽中，也不会被其它 token 取代。因此，用户只需要关注每个区块中存储属于自己的 token 的状态，完全不用关心别的插槽存储的内容。

在实际的 Plasma Cash 区块中，使用稀疏梅克尔树来存储每个插槽的内容，

### 稀疏梅克尔树

### 交易

### 取款

### 攻击场景

### 相关项目

> Talk is cheap, show me your code.

目前已经有许多机构和公司已经实现了 Plasma Cash，但实现的语言和细节有所不同：

* Loom Network

### 总结

### 相关资源

1. [https://ethresear.ch/t/plasma-cash-plasma-with-much-less-per-user-data-checking/1298](https://ethresear.ch/t/plasma-cash-plasma-with-much-less-per-user-data-checking/1298)
2. [https://en.wikipedia.org/wiki/Non-fungible_token](https://en.wikipedia.org/wiki/Non-fungible_token)
3. [http://erc721.org/](http://erc721.org/)
4. [https://github.com/ethsociety/learn-plasma](https://github.com/ethsociety/learn-plasma)

