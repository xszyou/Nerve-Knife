# Nerve-Knife



![](qrcode.png)



获取**源码**请进行知识星球：Easy Deal

注：首先强调投资有**风险**，本文仅作技术算法交易，不能作为入市依据。若对你有任何帮助，请不忘为本文点赞

![img](https://img-blog.csdnimg.cn/f744b3e287d143c08b66773de296f81c.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑



​    在开始本文之前首先明确我的几个交易上的价值观，若你不认同，可跳过下面精采的5000字了（为什么是5000？多少字，这不重要，在此我只是向中华文明致敬，并希望以自己从事信息化解决方案多年的经验为中国金融献出一点思想）。我的核心价值观如下：

1. 金融交易是一个**复杂系统**，轻微的差别导致结果大相径庭。复杂系统是一个科学研究的领域术语，意为不能通过部分还原整体的行为。比如：人就是一个复杂的系统，你不能通过计算细胞的行为来推测出人的情绪。金融交易作为复杂系统，导致的结果是：完全相同交易策略的机器，甚至跟着某个大牛的交易信号，最终赢利情况也有很大差别。
2. 技术指标的用途是告诉你现在处于什么状态，并**不能预测未来**，你永远不知道下一刻会发生什么。几乎所有技术指标都能准确反映过去的行情。为什么呢？因为其只是用了些不同的数学（统计学）方法直观的告诉了你：过去发生了什么。而现状是由过去导致的，故指标是能够反映现状的。若你通过技术指标知道现在是上涨行情，做多是正确的。问题是，你无法预知能涨到什么时候。下文我将说明我怎么去解决这个问题。
3. **顺势而为**,借势而进,造势而起,乘势而上！哈哈，其实我只想说，逆势加仓不是我的风格。



以下是5000字！会重点说明我的交易策略是如何做到一年翻3倍，及为什么不会爆仓。你也可以依此策略来编写量化交易程序。当然，mt4上的我已经编写完成，近期会考虑开源出来。其他交易系统也可以依此策略来编写。（刚刚收到消息，上交所的交易系统完成了升级，可以在10ms来完成一笔量化交易）

## 一、整体策略

我会使用m30做大趋势判断，m1做小趋势判断，实时行情变动作为走势判断（这里回应上文，技术指标表达过去的情况，只有当前价格变动才是最直接的反映，过去是客观的，未来很主观）。以下是整个策略的核心逻辑：

![img](https://img-blog.csdnimg.cn/8f60493ca8cd491087045287720835b7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

 顺的时候开仓加仓，不顺的时候减仓，这是不会错的。



## 二、合适的开仓量及开仓位置保可以快速盈利平仓，及低仓位过渡风险期

默认的参数是1000美元（美分）前5单的开仓是分别是：0.01手（1手100盎司）、不多于0.02手、不多于0.04手、不多于0.08手、不多于0.16手，第6单以顺势1000点就盈利平仓计算购买量。

当大趋势的技术指标与小趋势的技术指标一致且强烈，这说明这走势已经成形，并且很可能可以持续一段时间，是个开仓的好时机。这时侯，我选择的方式是再追踪几百点，看行情价格是否如指标反映再开仓。若已经有同向操作的仓位，开单的矩离大于550点，再开始追踪开创，减小开仓位置太集中的风险。

至于为什么是550点，这是我的技术指标判断小趋势行情的落差中位值是1810点。也就说有一半的情况，小趋势走1810点之后会反过来，这种反过来有可能预示着大的行情将要反转，我希望低仓位过渡(实际上大多情况下不超过1张单，下文会说明我是怎么做到，除非1盎司黄金的落差有1000美元，不然不会爆仓)。另外前5单也是成倍递增的，这是希望可以快速盈利平仓。

第6单是一张可以1秒救地球的单，我们改了个名字“海豹特击队”。若前5单一直顺势加仓都无办法盈利平仓，就在极其严格的条件下启动海豹特击队了：当前行情突破前3条m5 k线的最高价或最低价3%。

特别注意了，这里所说的盈利平仓是指，这6张单加起来盈利，并不是某一张单盈利。

## 三、3个仓位池设计确保不息工作

![img](https://img-blog.csdnimg.cn/63a65df119aa486ea25c5308d3a70a8a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

   趋势单是当前依把第二点描述加仓开仓的单，是盈利的主力（一个聪明的设计肯定不止一种赢利方式，哈哈）。但当技术指标判断大趋势（M30）已经反过来了，就得先把与新趋势下做单方向相反的单先锁起来，在新方向下继续依据第二点描述做单。此时锁定起来的单，形成锁定单仓位池。

   锁定单意思就是说之前行情是做多的，现在该做空了，那就不要在做多的方向上补单了。也不是说锁定后就不管它了，而是降低其盈利要求，只要它任何一张单独的单达到盈利1000点（即1美元），就开始追踪止赢，直到回撤300点（0.3美元），就盈利平仓。这样做一方面可以有一定机率再次降低风险的仓位（简单逻辑，开仓最大的单总是先盈利,而且更有趣的是有一定机率转向的时候整体浮亏，最后的单是浮盈的），另一方面是不要错过任何一个盈利的机会。

   最后要说的是保留单。做多做空再做多，那么原来因转换趋势而锁定的做多订单就得捡起来了。但此时有可能捡起来的订单，开单价与现时行情差矩太大，这样会导致快速补到4、5张单，也不能快速平仓，高仓位风险就来了，而且浪费行情。更糟糕的情况是，还未平仓，趋势又转了，这下一下子就会锁住非常高的仓位了。保留单仓位池就是解决这个问题的，锁定的单开仓价与行情价差太大，就先忽略它，做趋势单。直到价差小于3000点（假设第5张单与行情差3000点，此时浮亏大约是10%了），就按对应的开单方向转入锁定池或趋势池。

​    另外，保留单有可能会保留很长时间，这不用担心。若理解了上面描述的，你应该知道，保留单基本都是低仓位的单，而且双向都有。首先，这在一定程度已经自带对冲功能了，其次行情总会向某一方向走，时间长了终会解除保留的。再者，按1盎司黄金落差100美元（100！）算，最多会形成双向的6张单（我预留10个坑位），最大浮亏也不超过30%。这是浮亏，不是真亏，就放着，让它跑回来就行了。还有，若你发现一张0.01手的单进入了锁单池或保留单并浮亏越来越大，请忽略它，总有机会让它盈利的。退一万步说，这张单能让你爆仓的条件是每盎司黄金上涨或下跌1000美元，但若真能有1000美元幅度，你会赚到笑。若双向都有单，那就真不用担心，自觉形成对冲了，哈哈。



## 四、三档移动止赢机制设计确保利润最大化

![img](https://img-blog.csdnimg.cn/30ea14df78ac4b0792cd8a8f522f0061.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

  这是一个标准的移动止赢机制，比如第1档：当前趋势的订单总浮盈达到1000点（3美元）开始追踪，如果一直上涨，上涨到10美元、30美元都不会平仓，直到从最高点减少500点（0.5美元）才平仓。

   这里特别的是，我设计三档移动止赢机制，这三档都只是对趋势单有效。（实质上非趋势单是不会触碰到）



## 五、大小趋势加管壁突破互相咬合的技术指标再次降低风险

![img](https://img-blog.csdnimg.cn/2227b5596e134c75afddc800a19f0234.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

  大小趋势(m30及m5)判断是结合hiken ashi smoothed 及macd技术指标,但大小趋势的判断准则上略有不同。

  大趋势要稳定，否则短暂的反向可能会导致反向订单的产生，造成反向仓位风险。看上图尾段has绿色的位置，若这图是在m30上的，则会判断为弱趋势，不改变做单方向，当然也不会再继续加仓。直至macd柱（看前一条k线）走到零轴上方并且has是绿色（看前一条k线），这时候才会判断为上升。这样以has为主，通过macd的组合为大趋势滤波，可以稳定平均时间在9小时以上的一波大行情。如图上红框都会稳定做sell单。

  小趋势要反应敏捷，在顺势时果段加仓，快速实现趋势单盈利平仓，在逆势时果段减仓降低风险。同样，看上图尾段has绿色的位置，若这图是在m5上的，则会判断为上升，只要macd柱在singnl线上方（看当前k线），并且has绿（看当前k线）即可。要敏捷为什么不用m1呢？因为我们还需要稳定一小段时间让ea有足够时间去赢利平仓。

  也有小趋势上has与macd判断是相反的时候，这时候其实是个振荡期，已经一定机率预示小趋势会反转，真进一步说，有一定机率预示着大趋势也会反。也就是做单方向可能需要反过来了。所以做小趋势变弱开始，就会追踪盈利减仓了。和上面说的一样，盈利一单追踪止赢减一单。

  这里还有一问题，就是如我价值观2所说的，技术指标是过去的反映。假若当前金价突破大涨或者跳水，技术指标是来不及反映的。这里我通过5条1分钟k线反向突破管壁开仓不加仓的策略去识别。管道壁这个思路来源于这个ea的指导者，也是发起人（下文会提及），这是行家的20年经验。下图1引自我与他的联天记录。当前后来，我通过一些数学方法验证其实是有科学根据的，下图2是我用python输出最近一周的区间突破值的散点图。横坐标是向下突破值，纵坐标是向上突破值，红色是我的m5组合判断为下降，绿是上升，蓝是弱趋势。有趣吧，一周38万个行情数据，38万个点，形成了一线直线。得出的道理很简单，蓝点弱趋势是行情反转概率最高的地方，在这地方不加仓（趋势下第2单之后）就是了。但开仓，若不开仓这么会让ea非常安全，但也经常不做单。上文说过了：其实低仓位那怕行情反转也无关系。

 ![img](https://img-blog.csdnimg.cn/69d1d6e640264627b728cd1e15811756.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

![img](https://img-blog.csdnimg.cn/d5fabd5a94264e26a2d06c26eeaca552.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

   还有一件有趣的事：has默认是用6条k线做移动平均线的，6条5分钟的k线刚好30分钟。然后我再用5条1分钟线来做行情的管壁突破。这会不会是一个非常严紧的趋势判断组合呢？ 



## 六、印象深刻的一些失败的试验

1. 选用更敏感的指标及更快的k线。
2. 浮亏过大对冲控制风险。

不细说了，主要原因是现在是北京时间9月1日17点31分。

![img](https://img-blog.csdnimg.cn/f9b80529ecfc43b1b7787b2880392b39.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑





## 七、感谢及补充说明

​    上文很多数据计算是按1000美元的本金算的，实际我的ea设计复利机制。进入了量化交易，你就得适应与浮亏共存，只要一开仓浮亏就存在，当盈利了就平仓，这是本策略的运作机制。

  本ea的开发及测试是从7月22日开始（为什么我记得清楚，因为这是我的机器上MT4最早的复盘数据），到本文编写完成，相熟的个别朋友已经在实盘上盈利了。1个月可以完成开发，不是强调我的编码能力有多强（哈哈，自信还是有的），而是因为我们有很强的行业专家作经验指导。这里要感谢贾总把20年经验变成一页页的a4文档，实际上在我刚开始编码时，我连什么是浮亏都得问。也要感谢锋哥、kj等人的支持，凭信任直接上实盘测试，也给了很多有价值的反馈。

同时我也想向同事证明，我们公司定位：不挑行业“做最好的信息化解决方案”，是可行的。我们差了的经验，我们的合作伙伴有，我们只需要做好信息化的这一块即可！对了，还得感谢一本书《金字塔原理》。依靠文字描述是无法达到编码的严紧级别的，这它的mice法则，是它的金字塔结构思想，让我理顺及补充每一种可能的情况。故，我也要咱们的每一个同事必须认真读一遍。



## 八、nk的版本升级日志证明我是怎么走过来的。

![img](https://img-blog.csdnimg.cn/4aacf1a5ea924e82a0262e51e019d97f.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

![img](https://img-blog.csdnimg.cn/23937fdbfeb44289b88b63435d382e38.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑





