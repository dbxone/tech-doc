


# dbxui introduction

DBXChain data transaction client, dbxui, is a client deployed on merchants and local data source and developed based on Nodejs, so merchants and data source could sell and buy their data by local call, and the the whole-process parameter of data transaction as well as the replying data are encrypted, which is however simplied by dbxui.

# Installment environment

dbxui is developed based onNodejs, and its execution evironment is Ubuntu16.04. dbxui needs to install Nodejs8.0 or the above version.

## Install nodejs

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
apt install -y nodejs
node -v
npm -v
```

## Set up npm source
vim ~/.npmrc

```
registry=https://registry.npm.taobao.org
sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
phantomjs_cdnurl=http://npm.taobao.org/mirrors/phantomjs
ELECTRON_MIRROR=http://npm.taobao.org/mirrors/electron/
```

## Install yarn
```
npm i -g yarn
```

## Download and install dependence package
```
git clone https://github.com/dbxone/dbxui
cd dbxui
yarn
```


## Modify the service node

```
vim dbxui/app/api/apiConfig.js
```

```
{url: ws://ip:port", location: "Locally hosted"}
DEFAULT_FAUCET: "http://ip:port",
```
Modify the ip and port in these two lines to the address and endpoint of the private chain

## Start development mode

```
npm start
```
