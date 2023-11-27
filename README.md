# mosdns DNS服务器支持分流部署
- mosdns 使用V4.5.3
- easymosdns 使用v1.0.0
- AdGuardHome 使用最新版本
https://github.com/AdguardTeam/AdGuardHome

使用Docker实现分流
## 基础使用原理介绍
- AdGuardHome使用 53 端口进行DNS接入及广告过滤；
- 上游转发至MOSDNS 6553端口，MOSDNS通过上游进行DNS分流；
- 普罗米修斯实现对MOSDNS的服务状态监控。

##端口配置
|服务|端口01|端口02|说明|
| ---------- | :-----------:  | :-----------: | :-----------: |
|MOSDNS|9080(服务侦测)|6553（UDP/TCP）|
|easymosdns|
|AdGuardHome|3444（http）|53（UDP/TCP）|
