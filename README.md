# Compose

本仓库记录了我在VPS中使用docker部署多项服务的compose文件
安全起见，服务器**只暴露**ssh端口和80/443端口
所有的服务通过Nginx反向代理，通过443端口访问，通过不同的域名来区分。

各个项目都只在同一个docker网络中存在，这样方便不同的容器间相互访问。
手动指定每个容器的ip，目的是服务器重启后，ip不会变化。

0. 默认已经安装好Docker/Docker compose

1. 首先创建一个名为`npm_dafault`的bridge网络
```bash
docker network create --subnet=172.20.0.0/24 npm_dafault
```
2. 使用Nginx Proxy Manager来管理所有反向代理

    其中81端口为NPM的管理后台端口，配置好以后也隐藏起来。

3. 使用dockage管理compose文件

    其中`compose.yml`为配置好的文件，`.env`文件为默认环境变量文件

4. 启动各个服务
```bash
docker compose up -d
```
