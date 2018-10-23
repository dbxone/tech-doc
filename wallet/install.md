


# dbxui介绍

DBXChain数据交易客户端dbxui是基于Nodejs开发的一个部署在商户和数据源本地的客户端，商户和数据源可以通过本地调用的方式购买和出售数据，数据交易的全程请求参数和回传数据都是经过加密处理的，而dbxui简化了这样的一个流程。

# 环境安装

dbxui基于Nodejs开发，执行环境为Ubuntu16.04。dbxui需要安装Nodejs8.0以上版本.

## 安装nodejs

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
apt install -y nodejs
node -v
npm -v
```

## 配置npm源
vim ~/.npmrc

```
registry=https://registry.npm.taobao.org
sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
phantomjs_cdnurl=http://npm.taobao.org/mirrors/phantomjs
ELECTRON_MIRROR=http://npm.taobao.org/mirrors/electron/
```

## 安装yarn
```
npm i -g yarn
```

## 下载及安装依赖包
```
git clone https://github.com/dbxone/dbxui
cd dbxui
yarn
```

## 开发模式启动

```
npm start
```