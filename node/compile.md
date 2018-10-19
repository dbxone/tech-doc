# 源码编译安装

DBXChain见证节点`witness_node`和命令行钱包`cli_wallet`都是通过源码编译安装来完成的。

## 环境要求
* 系统: Ubuntu 16.04 LTS 64-bit, 4.4.0-63-generic 内核或更高
* 内存: 8GB+
* 硬盘: 100GB+

## 依赖安装

openssl依赖版本1.0.x ; boost依赖版本1.57.0。

```
sudo apt-get update
sudo apt-get install -y autoconf cmake git libboost-all-dev libssl-dev g++ libcurl4-openssl-dev unixodbc-dev libjsoncpp-dev uuid-dev build-essential
```

## 下载源码，编译，安装

```
git clone https://github.com/dbxone/dbxchain.git
cd dbxchain
git checkout <tag>
git submodule update --init --recursive
mkdir build ; cd build
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo -DCMAKE_BUILD_TYPE=Debug ..
make
sudo make install
```

