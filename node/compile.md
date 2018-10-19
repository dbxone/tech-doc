# 源码编译安装DBXChain见证节点和命令行钱包

目前支持ubuntu16.04 LTS。

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

