# 10-21 some ideas for media transmission

发送端根据拥塞控制算法反馈的交付速率，决定合适的传输码率的视频块。

ABR算法则是根据本地数据块下载的速率，决定向服务器请求不同码率质量的视频片段。

ABR算法广泛应用于点播的原因是它是一个服务器对很多客户端，服务器发送端无法为每一个连接计算流量，并选择最合适的视频块。所以不如直接从客户端判断网速，并向服务器发出请求。

如果要做发送端自适应码率传输，则必须是p2p连接或者客户端很少的情况。所以用quic做自适应码率传输有意义吗？可以部署在推流端，从编码器推到CDN。这样的话，可以保证低延迟，但是质量未必稳定。

关键点：

- 根据拥塞控制反馈的带宽控制选择的视频编码速率
- 修改协议重传机制，在丢包环境下，可以容忍部分数据的丢失，也要保证低延迟
- 数据包排队策略和接收后重新排序问题，以及播放ddl和重传的处理
- 拥塞控制机制的改进？