# DBXChain



.DBXChain is the DBX blockchain implementation and command-line interface. Current binary version of the DBXChain software for ubuntu 16.04 LTS, see [here](https://github.com/dbxone/dbxchain/releases).Visit [dbx.io](https://www.dbx.io/) to learn about DBX.

# 

# 

## 安装环境

A decent C++11 compiler \(GNU GCC 5.4.1+ on ubuntu, or Apple LLVM version 8.1.0 \(clang-802.0.42\) on MacOS\). CMake version 2.8+. Boost version 1.57.0. The repository contains the install scripts for gcc5 and boost 1.57.0, see [here](https://github.com/dbxone/dbxchain/tree/master/script).

```
# dependencies for OS X, macOS Sierra 10.12.6 recommended
brew install openssl cmake git openssl autoconf automake doxygen autoreconfls libtool

# dependencies for ubuntu 16.04 LTS
sudo apt-get install cmake make python-dev libbz2-dev libdb++-dev libdb-dev libssl-dev openssl libreadline-dev autoconf libtool git ntp
```

### For OS X

OS X Build Instructions

===============================

1. Install Homebrew by following the instructions here:[http://brew.sh/](http://brew.sh/)

2. Initialize Homebrew:

   ```
   brew doctor
   brew update

   ```

3. Install dependencies:

   ```
   brew install openssl cmake git openssl autoconf automake doxygen autoreconfls libtool wget
   ```

4. Install boost 1.57

   ```
   wget 'https://raw.githubusercontent.com/dbxchain/dbxchain/master/script/boost_install.sh' -O boost_install.sh
   bash boost_install
   ```

5. Build DBXChain:

   ```
   git clone https://github.com/dbxone/dbxchain.git
   cd dbxchain
   git submodule update --init --recursive
   cmake -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl -DOPENSSL_INCLUDE_DIR=/usr/local/opt/openssl/include -DOPENSSL_LIBRARIES=/usr/local/opt/openssl/lib -DCMAKE_BUILD_TYPE=RelWithDebInfo .
   make
   ```



### FOR Linux （Ubuntu）

Ubuntu 16.04 LTS Build and Install Instructions

===============================

1. Install gcc5

```
sudo apt-get install software-properties-common

# install gcc5 on ubuntu 16.04
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install gcc-5 g++-5
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 60 --slave /usr/bin/g++ g++ /usr/bin/g++-5

```

1. Install dependencies:

```
sudo apt-get install cmake make python-dev libbz2-dev libdb++-dev libdb-dev libssl-dev openssl libreadline-dev autoconf libtool git ntp

```

1. Build Boost 1.57.0 The Boost which ships with Ubuntu 16.04 is too old. You need to download the Boost tarball for Boost 1.57.0.

```
wget 'https://raw.githubusercontent.com/dbxchain/dbxchain/master/script/boost_install.sh' -O boost_install.sh
sudo bash boost_install.sh

```

1. Build DBXChain

```
git clone https://github.com/dbxone/dbxchain.git
cd dbxchain
git submodule update --init --recursive
cmake -DOPENSSL_ROOT_DIR=/usr/bin -DOPENSSL_INCLUDE_DIR=/usr/include/openssl -DOPENSSL_LIBRARIES=/usr/lib/openssh -DCMAKE_BUILD_TYPE=RelWithDebInfo .
make
```



