# 源码编译安装DBXChain

DBXChain见证节点`witness_node`和命令行钱包`cli_wallet`都是通过源码编译安装来完成的。

## 环境要求
* 系统: Ubuntu 16.04 LTS 64-bit, 4.4.0-63-generic 内核或更高
* 内存: 8GB+
* 硬盘: 100GB+

## 依赖安装

* DBXChain智能合约需要clang编译器支持；
* openssl最低依赖版本1.0.x ; 
* cmake最低依赖版本3.11.0；
* boost最低依赖版本1.67.0。

注: 以下操作，加入您已经获取了root权限。

## 安装依赖包

```
apt update
apt -y install software-properties-common
apt-add-repository "deb http://apt.llvm.org/trusty/ llvm-toolchain-trusty-4.0 main"
add-apt-repository ppa:ubuntu-toolchain-r/test
apt update
apt -y install clang-4.0 lldb-4.0 libclang-4.0-dev wget make python-dev libbz2-dev libdb++-dev libdb-dev libssl-dev openssl libreadline-dev autoconf libtool git ntp doxygen libc++-dev cmake  g++ libcurl4-openssl-dev unixodbc-dev libjsoncpp-dev uuid-dev build-essential libstdc++-7-dev
```

## 安装cmake
```
cd && wget https://cmake.org/files/v3.11/cmake-3.11.0-Linux-x86_64.sh
mkdir -p /opt/cmake && chmod +x ~/cmake-3.11.0-Linux-x86_64.sh
bash ~/cmake-3.11.0-Linux-x86_64.sh --prefix=/opt/cmake --skip-license
ln -sfT /opt/cmake/bin/cmake /usr/local/bin/cmake
```

## 安装 boost 1.67
```
wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.gz -O  boost_1_67_0.tar.gz
tar -zxvf boost_1_67_0.tar.gz && cd boost_1_67_0 && chmod +x bootstrap.sh
./bootstrap.sh --prefix=/usr
./b2 --buildtype=complete install
```

## 安装llvm
```
mkdir  ~/wasm-compiler && cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd .. && mkdir -p build && cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=~/opt/wasm -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ..
make -j4 install
```

## 编译安装
```
git clone https://github.com/dbxone/dbxchain
cd dbxchain
git submodule update --init --recursive


export WASM_ROOT=~/opt/wasm
export C_COMPILER=clang-4.0
export CXX_COMPILER=clang++-4.0

mkdir -p build &&  cd build
cmake -DWASM_ROOT=${WASM_ROOT} -DCMAKE_CXX_COMPILER="${CXX_COMPILER}" -DCMAKE_C_COMPILER="${C_COMPILER}" -DCMAKE_BUILD_TYPE=RelWithDebInfo -DCMAKE_BUILD_TYPE=Debug ..

make -j4
make install
```