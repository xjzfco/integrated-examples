介绍：

除 v2ray（Xray） kcp 外，所用应用共用443端口。此端口由 caddy 监听（即 caddy 前置），反向代理 v2ray（Xray） 的 ws（WebSocket） 、 h2c 及 gRPC，若有 naiveproxy 就进行正向代理。包括应用如下：

1、vless-ws-tls（tls由caddy提供及处理，不需配置；另可改成或添加其它ws类应用，参考反向代理ws类的单一示例。）

2、SS- v2ray-plugin -tls（tls由caddy提供及处理，不需配置。）

3、vless-h2c-tls（tls由caddy提供及处理，不需配置；另可改成或添加vmess-h2c-tls应用，参考反向代理h2c的单一示例。）

4、vless-grpc-tls（tls由caddy提供及处理，不需配置；另可改成或添加vmess-grpc-tls应用，参考反向代理grpc的单一示例。）

5、vless-kcp-seed（可改成vmess-kcp-seed，或添加它。）

6、naiveproxy （带有forwardproxy插件的caddy才支持naiveproxy应用，否则仅上边应用。tls由caddy提供及处理。）

注意：

1、Xray 版本不小于 1.4.0 或 v2ray 版本不小于v4.36.2，才完美支持 grpc 应用。

2、caddy 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray（Xray） 的 h2c（gRPC） 反向代理。

3、使用本人 github 中编译好的 caddy 文件，才可同时支持 naiveproxy、h2c proxy 等应用。

4、caddy 的 Caddyfile 配置与 caddy.json 配置二选一（效果一样）。支持自动 https，即自动申请与更新证书与私钥，自动 http 重定向到 https。

5、支持 ws（WebSocket）与 grpc 的 CDN 加速。

6、配置1：全部端口转发。配置2：vless-ws-tls应用进程转发，其它端口转发。