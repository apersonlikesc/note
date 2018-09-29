### day6 基础

网络层连接的两种方式:
  - 虚电路vc:可靠通行由网络层来保证需要建立连接,**通信时只需要虚电路的编号**,按发送顺序到达终点(和打电话一样建立了连线)
  - 数据报:可靠传输由主机中的**运输层**(差错处理,流量控制)保证,**每个分组独立发送
**
和ip协议配套使用的还有三个协议:`arp` `igmp` `icmp`

网络是多种多样的,将网络相互连接起来需要不同的连接设备:
  - 物理层使用**转发器**
  - 数字链路层使用**网桥,桥接器**
  - 网络层使用**路由器**
  - 网络层以上协议使用**网关**

转发器和网桥或者桥接器只是将网络扩大了,网络连接一般使用路由器
只要每个网络**使用**的是**相同的ip协议**,就可以将相互连接的网络组成一个**虚拟互联网络**(逻辑上)(通过路由器进行转发)
每个网络的异构性是**客观曾在**的
ip地址是**惟一**的

分类的ip地址:网络号+主机号:
- A类:八位网络号(0+7位)+(24位)主机号 单播 从1开始
  -  网络号数:除去全是0和127
  - 主机号数:除去全是0 和 全是1
-  B类:16位网络号(10+14位)+(16位)主机号 单播 从128.1开始
  -  网络号数:除去128.0.0.0
  -  主机号数:除去全是0 和 全是1
-  c类:24位网络号(110+21位)+8位主机号 单播 从192.0.1开始
  -  网络号数:除去192.0.0.0
  -  主机号数:除去全是0 和 全是1
-  d类:1110+多播地址 多播使用
-  e类:1111+.... 保留

每次**连接一个网络就需要一个ip地址**,网络号必须是不同的
**ip地址指向** 的不一定是主机,还可以是其他(比如**一个路由器**)
不同网络号的局域网必须使用路由器进行连接
同一局域网具有同一网络号
通常如果两个路由器之间出现的网络(一条连线)叫做**无编号网络**

ip数据报里面的**源地址**和**目的地址**在转发中是**不变**的,而**mac地址是不断变化的**,不断的丢弃和封装
路由器根据ip的目标地址进行转发,ip层只能看到ip数据报,局域网的链路层只能看见mac帧

**arp协议**:
  - 主机(路由器)中有一个arp高速缓存器,里面存放ip地址和mac地址的映射,**会定时的更新删除**
  - 假如这个缓存器里面**找不到映射**的话,那么主机(路由器)就发送arp的请求给该主机(路由器)所在的局域网**所有**主机(路由器),
  - arp请求里有寻找的ip地址,如果这个ip地址的主机收到了这个请求包,就**单播**给源ip地址告诉他信息,映射就储存下来了(**双方都储存**)

**ip数据报**:首部(固定20字节+可变附加部分)+数据
>固定20字节可分成4个字节的5段
>
- **第一段**:`版本`(**ip协议版本**)+`首部长度`(**4个字节的整数倍**)+`区分服务`(**一般不使用**)+`总长度`(**首部与数据之和的长度**)
- **第二段**:`标识`(**分片时使用**,**相同的标识字段的值使分片后的各数据报分片能正确组装**)+`标志`(**占3位,目前使用两位,中间df `0` 不分片 `1` 分片,低位 `1` 后面还有分片 `0` 后面没有分片了**)+`偏移量`(**表示这个分片是从什么地方开始的,相对于原来的全长数据报,开始的地方/8,比如从1200开始就是1200/8,如果后面的分片又分片了,也要加上前面的距离,比如(1200+300)/8)**
- **第三段**:`生存时间`(ttl,**跳转限制**)+`协议`(**使用的协议**)+`首部检验和`(**只检验数据报的首部,将首部分成若干个16位的段,加起来去反,检验和是16位,估计是去掉高位,之后检验的时候和现在一样,结果是0就保留**)
- **第四段**:`源地址`
- **第五段**:`目标地址`