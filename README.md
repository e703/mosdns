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
|easymosdns|统计插件|
|AdGuardHome|3444（http）|53（UDP/TCP）|
|普罗米修斯|3000（http）|



```
chmod +x dns*.sh
./dns*.sh

crontab -e

在文件末尾添加以下内容
0 5 * * * sudo truncate -s 0 /etc/mosdns/mosdns.log && /etc/mosdns/rules/update-cdn
#每天5点升级域名库并清除mosdns日志文件
```
