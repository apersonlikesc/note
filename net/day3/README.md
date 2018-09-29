## day3基础

信道是**单向**的

**基带信号**:
  - 来自信源的信号称为基带信号,比如计算机输出的各种文字,图像文件的数据.
  - 往往包含有较多的低频成分,甚至直流成分,但是某些信道不能传输,所以要进行调制

**调制**:
  - 基带调制,仅仅对基带信号的波形进行变换,使之能有在信道上传输,转换成另外一种数字信号
    不归零,归零,曼切斯特,差分漫切斯特
  - 带通调制:使用载波进行调制,经过载波调制的信号称之为带通信号
    - 调幅(振幅),调频(频率),调相(初始相位)

码元传输的**速率越高**,或信号传输的**距离越远**,**噪声干扰越大**,**传输媒体质量越差**,波形的**失真越严重**

信道能通过的频率是**有限**的

在任何信道中,码元传输的速率是**有上限**的,传输速率超过此上限,就会出现严重的**码间串扰**(码元不明显),使接受端无法使别

信噪比:信号的平均功率和噪声的平均功率之比

信道的带宽或者信道中的信噪比越大,信息的极限传输的速率就越高_(香农公式可以计算出信道的极限信息传输速度)_

- 传输媒体:
  - 导引型传输媒体(固体媒体)
  -  双绞线,绞合可以减少对相邻导线的电磁干扰
  -  同轴电缆
  -  光缆:光纤,有单模光纤(单光)与多模光纤(多光,不同角度)之分
  -  架空明线:铜线和铁线
- 非导引型传输媒体(自由空间)
    - 卫星通信有较大的传播延迟
    - 微波是直线传播的,因此需要中继站
    - 短波主要靠电离层的反射,但是质量较差
    - 无线传输

信道复用技术:
  - 频分复用:在相同的时间占用不同的带宽资源**(频率不同,并排)**
  - 时分复用:在不同的时间占用相同的频带宽度**(时间不通,排队)(利用不高)**
  - 统计时分复用:按需分配时间段,每个时间段中要有用户的地址**(前提用户必须间歇的工作)**
  - 波分复用:光的频分复用
  - 码分复用:相同时间,相同频率,不同的码型,每一个比特时间被分成m(64/128)段间隔(码片),每一个站分配的码片是**不同**的,而且必须**正交**

>时分复用更有利于数字信号的传输


数据链路层使用的信道有两种类型:
  - 点对点信道:使用一对一的点对点信道通信方式
  - 广播信道:使用一对多的广播通信方式

路由器在转发分组的时候使用的协议站只有**下面的三层**

链路:一个结点到相邻结点的一段**物理线路**
数据链路:将**协议**和**硬件**加到链路上就构成了数据链路.

>一般的适配器包含了数据链路层和物理层的功能

数据链路层将网络层交下来的数据构成帧发送到链路上,并且接受帧传递给网络层

帧是点对点信道的数据链路层的协议数据单元,ip数据报(包,分组)是网络层的协议数据单元,可以理解成**(当前协议下的)** 被接受的数据单元