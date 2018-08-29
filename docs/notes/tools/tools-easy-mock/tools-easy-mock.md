# Easy Mock 本地搭建

## 依赖

Node.js (>= v8.9)

MongoDB (>= v3.4)

Redis（>= v4.0）

这里 MongoDB 和 Redis 我们都可以直接使用 docker 创建

## 安装

```
git clone https://github.com/easy-mock/easy-mock.git
```
安装依赖

```
npm install
```

## 配置

复制 config/config.json 重命名为 local.json

其中 db 和 redis 配置成我们 docker 的地址

![图片描述](./tools-easy-mock/01.png)

## 启动

```
npm run dev
```