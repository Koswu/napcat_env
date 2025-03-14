# NapCat Env

用于在 Linux 服务器上搭建 [NapCatQQ] 提供的 [OneBot] 服务，提供给 [NoneBot] 项目使用

## 部署方式

```
echo "ACCOUNT=[你的qq号]" > .env # 设置要登录的 qq 号作为环境变量传入
docker network create onebotnet # 如果没创建的话创建一个网络
sudo docker-compose up -d
```

### 第一次执行

如果是第一次执行，需要扫码登录，通过 `docker-compose logs` 查看二维码

PS: 取决于 qq 的逻辑，也可能每次重启容器都需要扫码登录，这也是为什么要独立这个服务的原因（不希望更新一次逻辑就要扫码）


## 对外暴露的使用方式

管理：可以通过本机的 6099 端口 [OneBot] 服务，访问 http://localhost:6099/webui/login.html 即可管理 (和直接部署 NapCat 一致)

nonebot 连接：其他容器加入 `onebotnet` 这个 [docker network](https://docs.docker.com/network/) ，即可通过 ws://napcat:3001/ 连接，即 onebot 标准的[反向 WebSocket 方式](https://12.onebot.dev/connect/communication/websocket-reverse/)

## 为什么要拆分单独的项目？

因为期望 NCQQ 服务不经常更新，而 [NoneBot] 的代码可以随时更新，这样可以在不重启服务的情况下更新机器人逻辑。

如果你没有这个需要，那其他一键部署脚本可能更适合你。

[NoneBot]: https://nonebot.dev/
[OneBot]: https://onebot.dev/
[NapCatQQ]: https://github.com/NapNeko/NapCatQQ
