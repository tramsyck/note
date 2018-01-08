# 数据库
## StateDB
包含在以太坊协议内，在merkle上存储数据。负责缓冲和存储嵌套的状态。
主要提供的查询接口是:Contracts和Accounts，即合约和账户。

## Receipt
其中有一个Log类型的数组，其中每一个Log对象记录了Tx中一小步的操作。所以，每一个tx的执行结果，由一个Receipt对象来表示；更详细的内容，由一组Log对象来记录。这个Log数组很重要，比如在不同Ethereum节点(Node)的相互同步过程中，待同步区块的Log数组有助于验证同步中收到的block是否正确和完整，所以会被单独同步(传输)。
Receipt的PostState保存了创建该Receipt对象时，整个Block内所有“帐户”的当时状态。Ethereum 里用stateObject来表示一个账户Account，这个账户可转帐(transfer value), 可执行tx, 它的唯一标示符是一个Address类型变量。 这个Receipt.PostState 就是当时所在Block里所有stateObject对象的RLP Hash值。
## Bloom
Bloom类型是一个Ethereum内部实现的一个256bit长Bloom Filter。 Bloom Filter概念定义可见wikipedia，它可用来快速验证一个新收到的对象是否处于一个已知的大量对象集合之中。这里Receipt的Bloom，被用以验证某个给定的Log是否处于Receipt已有的Log数组中。