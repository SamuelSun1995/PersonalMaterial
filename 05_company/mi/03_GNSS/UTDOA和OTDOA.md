# UTDOA和OTDOA

### 到达时间差（TDoA）

到达时间差（TDoA）技术，分为有线同步和无线同步，由于有线同步技术对布线和网络的要求较高，成本比较高，因此一般会采用无线同步技术，本文介绍的到达时间差（TDoA）技术都是基于无线同步。

标签将数据包发送到被基站覆盖的区域内，附近的所有基站都会收到标签的无线信号，但不会返回任何无线信号。由于基站与标签的距离间隔不同，因此消息在不同的时刻到达每个基站。这些时间差乘以空间中恒定的光速得到标签和基站之间的距离差，这样就可以形成多点定位计算的基础，从而确定标签的相对坐标。另外该技术的决定性因素是所有基站必须被同步。

基站之间同步和标签定位的无线数据包如下图所示：

![img](https://xiaomi.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=NjMyMmE3YzA5YTM1MDBhMWIwMjZkNjg3MzBkNTAwMmVfUjBXY2tWbFhzdThidHlGRXk3RDB0bnV6cGx5ajg3MnRfVG9rZW46Ym94azRpSG96a0R6c0plM2p4M3dGdTlOcm5jXzE2NzQ5NjExMDE6MTY3NDk2NDcwMV9WNA)

​                                        图 1-4 基站同步和标签发射定位流程图

得到各个基站的距离差之后，可以画[双曲线](https://www.zhihu.com/search?q=双曲线&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType":"answer","sourceId":2274991641})，同理交点就是标签的位置。

![img](https://xiaomi.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=MTEzY2YxMDUzMDc5MjM3ZGI3OWI1OGRmMDIyZWRlMjFfQVFYWXVKQ2w1OUdKeEx5VGJzQkhSbmVzVGdObUdmbzJfVG9rZW46Ym94azRIb2hlcHpPQjdlbGtwNEJmcTdkZWZnXzE2NzQ5NjExMDE6MTY3NDk2NDcwMV9WNA)

​                                              图 1-5 到达时间差方法定位流程图

基于ＴＤＯＡ测量的定位技术分：UTDOA和OTDOA。

UTDOA（上行到达时间差）移动终端发射上行测量信号，网络侧基站或者定位测量单元测量得到时间差。