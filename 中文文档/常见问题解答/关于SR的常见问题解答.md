
Private运行环境下full node模式的问题
-----
1. config.conf中的genesis.block.witnesses替换成在https://trxscan.org/ 注册时给出的address字符串：
  是否需要删除其他address？url和voteCount字段是否需要删除？
  
2. seed.node ip.list 替换成自己公网的ip地址后，使用启动命令 java -jar java-tron.jar 启动后，如何测试部署是否正常，比如是否有测试接口或者命令，类似redis，get ping 会返回 pong？


Private运行环境下super node模式的问题
-----
1. 在部署private 环境时，Super Node和Full Node 关系是什么样子？是否需要先部署Super Node ,然后部署Full Node ？

2. Private环境，因为我看官网是通过手动投票产生的SuperNode节点，是否还需要提交TRON资料审核注册成为Super Node节点？

3. 既然是Private环境，为什么日志还持续的更新全网其他节点，并同步保存信息？那么private 和public 的区别是什么？


public运行环境下的问题
-----

1. 单点的java程序最大能支持多少内存，cpu，处理请求等？

2. 这个网络流量大概是多少，我们是准备多台主机前面挂负载，还是提供多节点即可？

3. 对公网需要暴露那些服务端口？

   答：有：18888，50051

4. tokens 申请完成后，如何由not started yet 变更成 participate?


运行超级节点报错
-----
1. 以下错误信息表达了什么意思？

       17:02:42.699 INFO [o.t.c.s.WitnessService] Try Produce Block
       17:02:42.699 INFO [o.t.c.s.WitnessService] Not sync


超级节点出块问题
-----
1. 超级节点也是轮流出块的吗？出块间隔是多少？是不是24小时无心跳消息就从超级节点列表里删除了？

   答：轮流出，现在测试环境5秒一块，会统计超级节点出块miss率，出块率太低就会被投出局。

2. 在最坏情况下，万一超级节点无法联通，最多允许多长时间恢复服务？

   答：一个投票周期都可以恢复，但是出块率会被永久记录。

3. 超级节点出块miss率的计算公式是什么？
   
   答：主要统计"应该出但是没有出的块的个数"， 数量会一直累计，不会清除。

4. 超级节点服务器的测试版本，或者源码开放了吗？

   答：都是开源的，参见https://github.com/tronprotocol/java-tron。

5. 我怎样才能知道我的测试超级节点在运行了呢？

6. 另外，根据这个命令：java -jar java-tron.jar -p yourself private key --witness -c yourself config.conf(Example：/data/java-tron/config.conf，我怎样才知道运行的是超级节点？

7. 有什么命令行命令可以生成地址，发送tron的吗？一定要通过web wallet?

8. 我们要测试超级节点出块和性能的情况，是不是需要你们投票我们的节点才能竞选上？

   答：测试的时候，我们可以帮你么投票。

9. 那现在是不是可以看节点有没有出块了？

10. 请问刚上线是否出块时间是5秒一块？预计在什么时间会变成3秒1块？

    答：主网上线后会变成3秒1块。

11. 未来大概会有出块的TRX会减半的计划吗？如果有的话，大概在什么时间点？

    答：没有减半计划。

12. 当27节点中有一个 出现故障时，会自动检测并取消轮询资格吧？出现这种情况保留超级代表资格否？如果资格被取消后，何时可以恢复资格？

    答：会一直保留不出块的记录，其他人看了就不投了。


超级代表选举问题
-----

1. 为啥我刚才给自己的节点投了 2百万的 trx 投票，在 https://tronscan.org/#/network 看我自己的节点的投票数还是 0 trx 啊？

   答：每6小时统计一次，票数将在这一轮投票之后显示。
   
2. 持有的票数是和目前持有的TRX相等，每个TRX等于一票对吗。而且这个票可以投不止一个超级代表候选人？

3. 请问我们目前选的是否是100个超级代表候选人的资格？

   答：100个也是按照实际投票来的，目前就是预先选举，让有意向的节点，提前测试。

4. 这个需要用TRON来投票，是否代表我们需要在Tronscan钱包里存入一定数量的TRON？

   答：需要存，用来申请成为节点和投票。 

5. 针对每日选举的27个超级节点，是否有个门槛？还是鼓励自由竞争？

   答：自由竞争，拉票。  

6. 这27个超级代表获得的TRX是否是平均分配，还是是依据算力自由竞争？

   答：和机器算力无关，轮流出块。

7. 如果有大型矿厂参与竞选的话，是否有可能会出现算力超过50%的问题？

   答：不会。

8. 按照每秒出一个块的速度，出块的32TRX的奖励给对应出块的节点是吗？基于tron 公链的交易数量是否能达到每秒都有呢？

9. 细则里的社区支持方案具体是指什么？
   
   答：可以理解为计划多大的预算或者精力去发展社区。
   
10. 投票所用的trx是归属哪边？

    答：投票不会消耗trx。
    
11. 超级代表的权限只维持24小时吗？

    答：对，但如果投票情况没变 会一直维持下去。
    
12. build/resources/main/config.conf 和 wallet的build/resources/main/config.conf 两个配置节点里没有我的节点的任何信息,能识别我的节点并进行出块吗？

    答：配置文件需要改成您自己的私钥，然后投票成功，就可以出块了。
    
13. 我生成了自己的私钥以后怎样配置？

    答：配置文件里面有个localwitness，配成您投票账户的私钥。
   
   
其他问题
-----
1. RPC的接口文档在哪？

   答：https://github.com/tronprotocol/Documentation/tree/master/TRX

2. 咱们币安能否开一下USDT和BNB的交易对?

3. 启动节点的时候怎么制定数据存储目录？

   答：现在还不能制定数据目录，下一个版本会加。

4. 节点有钱包功能吗？

   答：节点有钱包的RPC接口，不能直接用命令行调用钱包功能，可以用另外一个repo里的命令行钱包使用full node的钱包功能。

5. 生成地址不需要按照文档里面自己生成私钥，计算生成地址吧？

   答：你注册一个账户后，不需要关心你的私钥，只要用pincode登入后就可以获取你的地址了。

6. API调用有没有更具体的文档，类似比特币或者以太坊的？

   答：我们的文档还在补充中，目前还不是很完善。我们刚补充了一份有关钱包rpc-api的文档在名为Documentation的repo里。

7. SolidityNode 和 fullnode可以装在同一台机器上吗？数据目录不能指定，两个节点会共用数据吗？有没有问题？

8. 没有Txid很麻烦，我们出金后怎么告诉用户 怎么查询出金交易？

   答：现在没有交易id和手续费，交易id功能正在开发中。

9. solidity是根据full同步区块的吗？

    答：是的。

10. geteway是链接solidity节点的吗？

    答：solidity节点主要目的是存储不可回退的固化块，会落后fullnode几个块，用来确认到账情况是比较合适的。用gateway链接solidity，或者连接fullnode，都能连接上。

11. listaccounts是全网所有地址吗？

    答：目前是的，还不确定会不会改，因为这个地址数量会很庞大，我们需要更多的沟通考量。

12. 余额小数位是多少？
    
    答：6位。

13. 节点的机器是否搭建在北京，会不会墙的问题？

    答：39.106.220.120在北京，其他的都在美国欧洲香港。

14.	用户可以通过将TRX存入tron.network向主网迁移吗？如果不行，还有哪些其他钱包支持迁移，还是只能由交易所经手？

    答：暂无钱包支持迁移，只能通过交易所。

15.	TRON现阶段有多少种钱包？

    答：据现有统计，我们已有命令行钱包、网页钱包，以及iOS钱包。我们相信在编程大赛之后，还会有更多设计精良的钱包。

16.	宽带需要达到25Gbps吗，还是10Gbps就足够？或者有其他的门槛？

    答：我们对网络宽带不做要求，给定的具体数据仅供参考。

17.	对于超级代表选举中排名27名开外但是100名以内的人，在当选的超级代表出局时，是由排名决定替补顺序，还是由特定算法决定接替人选？

    答：在测试网，我们仅是选出得票最多的27个节点。在主网及将来的测试网上，我们会使用另外的算法，增加超级代表产生的随机性。

18.	想要成为超级代表，我们只需要一个成熟的技术方案就可以，还是需要在提交申请前就搭建硬件？

    答：技术方案需要包含两个部分：1. 在6月26日即第一次选举之前的技术方案。2. 在6月26日即第一次选举结束之后的技术方案。第二部分只要有一个方案就可以。而第一部分，现阶段可以只有方案，但是只有具备了硬件条件，我们才能测试你的节点，其他用户也才能确认你们确实已经搭建起了测试节点。申请超级代表，并不等于能胜任超级代表。



































 