---
layout:     post
title:      使用docker安装单机RocketMQ
date:       2017-04-27
author:     BY stone
catalog: true
tags:
    - docker
    - docker-compose
    - RocketMQ
---

# 下载镜像

	docker pull registry.cn-hangzhou.aliyuncs.com/laizhenwei/rocketmq:4.2.0
  
# docker-compose启动

version: '2'
services:
  rocketmq: 
    image: registry.cn-hangzhou.aliyuncs.com/laizhenwei/rocketmq:4.2.0
    ports:
     - "9876:9876"
     - "10909:10909"
     - "10911:10911"
    environment:
     - "brokerIP1=本地ip"
    volumes:
      - '/Users/userName/data/rocketmq/store:/usr/local/rocketmq/store'

docker-compose up -d

# rocketmq-console

使用docker搭建rocketmq-console,界面控制台

version: '2'
services:
  rocketmq-console: 
    image: registry.cn-hangzhou.aliyuncs.com/aluomaidi/rocketmq-console-ng:1.0.0
    ports:
     - "32773:8080"
    environment:
     - "JAVA_OPTS=-Drocketmq.namesrv.addr=xxx.xxx.xxx.xxx:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false"
