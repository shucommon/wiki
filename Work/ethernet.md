ethernet:
	IEEE 802.3标准：
	IEEE于1980年2月成立了局域网标准委员会（简称IEEE802委员会）;
	IEEE 802.3规定了包括物理层的连线、电信号和介质访问层协议的内容。以太网是	 LLC 逻辑链路控制
	当前应用最普遍的局域网技术，她很大程度上取代了其他局域网标准。如令牌环、	 MAC 介质访问控制
	FDDI和ARCNET。
	CSMA/CD（Carrier Sense Multiple Access/ Collision Detect）即载波监听多路
	访问/冲突检测机制
	
	802.3以太网帧结构：
	前导码		帧开始符	mac目标	mac源地址 802.1q(可选) 以太类型或长度 负载	冗余校验 帧间距
10101010 7octs  10101011 1ocets 6octets	6octets	  4octets	2octets       46-1500 4 octets 12 octets
		72-1530 octets									 12
		84-1542 octets

	以太帧有很多种类型。不同类型的帧具有不同的格式和MTU值。但在同种物理媒体
	上都可同时存在。

	------------
	1. Ethernet V1
	2. Ethernet V2(ARPA)	6bytes + 6bytes + 2bytes
	3. RAW 802.3
	4. 802.3/802.2 LLC
	5. 802.3/802.2 SNAP

	Ethernet II:
	把紧接在目标和源MAC地址后面的这两个字节定义为以太网帧数据类型字段。
	802.3标准中以太网类型字段变成了一个字节长度。为了允许一些使用以太II版本
	的数据报和一些使用802.3封装的最初版本的数据包能够在同一个以太网段使用，
	以太类型必须大于1536(0x0600).这个值比802.3封包的最大长度150byte（0x5DC）
	要更大。因此如果这个字段的值大于等于1536，则这个帧是以太II帧，是类型字
	段。否则（小于1500而大于46字节），他是一个IEEE802.3帧，而那个字段是长度
	字段。1500～1536的数值未定义。
	在IEEE 802局域网体系结构中，数据链路层功能由LLC和MAC两个子层实现，LLC帧
	必须封装在MAC帧中进行传输，而不能单独地通过物理层传输。因此，LLC帧中没
	有用于帧同步的标志字段以及用于验证帧正确性的帧校验字段；这些字段由MAC协
	议添加在MAC帧中，而LLC帧被封装在MAC帧的信息字段中。MAC协议则与局域网类
	型有关。

	802.2 LLC
	这是IEEE正式的802.3标准，它由Ethernet V2发展而来。它将Ethernet V2帧头的
	协议类型字段替换为帧长度字段(取值0000-05dc；1500)；并加入802.2LLC头用以
	标志上层协议，LLC头中包含DSAP，SSAP以及Crontrol字段。

	802.2 SNAP
	IEEE为保证802.2 LLC上支持更多的上层协议同时更好的支持IP协议而发布的标准
	与802.3/802.2 LLC一样802.3/802.2 SNAP也带有LLC头，但是扩展了LLC属性，新
	添加了一个2Bytes的协议类型域（同时将SAP的值置为AA），从而使其可以标识更
	多的上层协议类型；另外添加了一个3Bytes的OUI字段用于代表不同的组织，RFC
	1024定义了IP报文在802.2网络中的封装发法和ARP协议在802.2SANP的实现。		IP在MAC中的封装方法。

	IEEE 802.2/802.3(RFC 1042)
        | <---- 802.3 MAC --> |<--802.2 LLC-->|<--802.2 SNAP-->|
	目的地址 源地址   长度  DSAP SSAP cntl org code 类型	数据	CRC
	 6	  6	   2	1	1 1	3   2		38-1492
							类型	IP数据报
							0800 
	以太网II的封装格式(RFC894)
	目的地址 源地址 类型 数据	CRC
	6	 6	2    46-1500

802.1q:
	16 bits	3 bits	1 bit	12 bits
	TPID	PCP	CFI	VID
	TPID = 0x8100(tag protocal identifier)标签协议识别符
	PCP = priority code point 优先权代码点
	CFI = canonical format indicator 标准格式指示
	VID = VLAN identifier 虚拟局域网识别符 0 - 4095，0x000 0xfff保留
