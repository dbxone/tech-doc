# Source code compiles and installs DBXChain

## Environment request
* System: Ubuntu 16.04 LTS 64-bit, 4.4.0-63-generic kernel or above
* RAM: 8GB+
* Hard drive: 100GB+

## Install dependence

* DBXChain smart contract needs the support from clang compiler;
* openssl's minimum dependence version is 1.0.x;
* cmake's minimum dependence version is 3.11.0;
* boost's minimum dependence version is 1.67.0.

## Install dependence packet

```
apt update
apt -y install software-properties-common
apt-add-repository "deb http://apt.llvm.org/trusty/ llvm-toolchain-trusty-4.0 main"
add-apt-repository ppa:ubuntu-toolchain-r/test
apt update
apt -y install clang-4.0 lldb-4.0 libclang-4.0-dev wget make python-dev libbz2-dev libdb++-dev libdb-dev libssl-dev openssl libreadline-dev autoconf libtool git ntp doxygen libc++-dev cmake  g++ libcurl4-openssl-dev unixodbc-dev libjsoncpp-dev uuid-dev build-essential libstdc++-7-dev
```

## Install cmake
```
cd && wget https://cmake.org/files/v3.11/cmake-3.11.0-Linux-x86_64.sh
mkdir -p /opt/cmake && chmod +x ~/cmake-3.11.0-Linux-x86_64.sh
bash ~/cmake-3.11.0-Linux-x86_64.sh --prefix=/opt/cmake --skip-license
ln -sfT /opt/cmake/bin/cmake /usr/local/bin/cmake
```

## Install boost 1.67
```
wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.gz -O  boost_1_67_0.tar.gz
tar -zxvf boost_1_67_0.tar.gz && cd boost_1_67_0 && chmod +x bootstrap.sh
./bootstrap.sh --prefix=/usr
./b2 --buildtype=complete install
```

## Install llvm
```
mkdir  ~/wasm-compiler && cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd .. && mkdir -p build && cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=~/opt/wasm -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ..
make -j4 install
```

## Compile DBXChain
```
git clone https://github.com/dbxone/dbxchain
cd dbxchain
git checkout contract
git submodule update --init --recursive


export WASM_ROOT=~/opt/wasm
export C_COMPILER=clang-4.0
export CXX_COMPILER=clang++-4.0

mkdir -p build &&  cd build
cmake -DWASM_ROOT=${WASM_ROOT} -DCMAKE_CXX_COMPILER="${CXX_COMPILER}" -DCMAKE_C_COMPILER="${C_COMPILER}" -DCMAKE_BUILD_TYPE=RelWithDebInfo -DCMAKE_BUILD_TYPE=Debug ..

make -j4
make install
```
