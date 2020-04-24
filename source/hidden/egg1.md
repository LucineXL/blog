---
title: egg1
date: 2020-04-22 17:43:27
tags:
---


1.  使用docker创建一个数据库

docker ps

docker images

docker run -d \
--name pg_db \
    -e POSTGRES_USER=monitor \
    -e POSTGRES_PASSWORD=monitor123 \
    -p 5432:5432 \
    postgres

    https://www.runoob.com/docker/docker-run-command.html

docker ps
docker stop 0d1a1f2eeb66


2. tabPlus  查看数据库

![](https://tva1.sinaimg.cn/large/007S8ZIlly1ge2ox244dsj30yk0padsp.jpg)

![](https://tva1.sinaimg.cn/large/007S8ZIlly1ge2p1zpkyjj30ri0nkwhw.jpg)
test -》 save

![](https://tva1.sinaimg.cn/large/007S8ZIlly1ge2p3ood4wj31hw0u04a3.jpg)
默认创建一个名称的数据库

3. egg.js
```
mkdir monitor && cd monitor
yarn global add egg-init
egg-init --type=simple
yarn
```

4. sequelize
https://eggjs.org/zh-cn/tutorials/sequelize.html
https://github.com/eggjs/egg-sequelize


npm install --save egg-sequelize
npm install --save pg pg-hstore

yarn add egg-sequelize pg pg-hstore


1.在 config/plugin.js 中引入 egg-sequelize 插件

2.在 config/config.default.js 中编写 sequelize 配置

3. yarn add sequelize-cli

4. .sequelizerc 配置文件

5. 初始化 Migrations 配置文件和目录
npx sequelize init:config
npx sequelize init:migrations

6. npx sequelize migration:generate --name=init-db

7. yarn sequelize db:migrate
![](https://tva1.sinaimg.cn/large/007S8ZIlly1ge2t68xn8aj31860oidm0.jpg)