---
title: Network - 网络协议
date: 2018-08-30 0:00:00
tags: Network
---
《圣经》中有一个通天塔的故事，大致是说，上帝为了阻止人类联合起来，就让人类说不同的语言。人类没法儿沟通，达不成“协议”，通天塔的计划就失败了。

千年之后,一群工程师为了解决这一问题,制定了各种协议与标准,让各种设备可以通过协议通信,进而通过互联网实现了让世界互联.


## 协议三要素

(1) 语义。每一段内容需要代表某种意义
(2) 语法。每一段内容符合一定规则的格式,
(3) 时序。每一段任务的执行顺序.

## 网络分层

网络分层就是将网络节点所要完成的数据的发送或转发、打包或拆包，控制信息的加载或拆出等工作，分别由不同的硬件和软件模块去完成。

简单的来说一个完整的HTTP请求,途中需要经过数次传送,期间需要不通的都软件与硬件模块去完成相应的工作.我们对相应的阶段的不通特性做出来相应的分类.每种网络分层,都有相应的协议标准做数据传送.

### 五层
物理层：以太网 · 调制解调器 · 电力线通信(PLC) · SONET/SDH · G.709 · 光导纤维 · 同轴电缆 · 双绞线等

数据链路层：Wi-Fi(IEEE 802.11) · WiMAX(IEEE 802.16) ·ATM · DTM · 令牌环 · 以太网 ·FDDI · 帧中继 · GPRS · EVDO ·HSPA · HDLC · PPP · L2TP ·PPTP · ISDN·STP 等

网络层协议：IP (IPv4 · IPv6) · ICMP· ICMPv6·IGMP ·IS-IS · IPsec · ARP · RARP等

传输层协议：TCP · UDP · TLS · DCCP · SCTP · RSVP · OSPF 等

应用层协议：DHCP ·DNS · FTP · Gopher · HTTP· IMAP4 · IRC · NNTP · XMPP ·POP3 · SIP · SMTP ·SNMP · SSH ·TELNET · RPC · RTCP · RTP ·RTSP· SDP · SOAP · GTP · STUN · NTP· SSDP · BGP · RIP 等