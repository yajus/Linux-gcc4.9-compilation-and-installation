# 第一步
### 首先下载gcc源码包
### wget http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-4.9.3/gcc-4.9.3.tar.bz2

# 第二步
### 将下载好的文件放在非root用户也有读权限的地方，例如 ~/myuser 或者 ~/gcc-build/ 下面第四步我会讲为什么要这么做.
### 这里我将gcc源码包放在了 */data1* 目录下

# 第三步
### 解压文件，做一些准备工作（编译安装gcc编译的依赖文件）

### tar xjvf gcc-4.9.3.tar.bz2
### cd gcc-4.9.3
### ./contrib/download_prerequisites

### 安装gcc需要5个组件，download_prerequisites 的任务就是下载这些组件分别是：

### ·*cloog-0.18.1*
### ·*gmp-4.3.2*
### ·*isl-0.12.2*
### ·*mpc-0.8.1*
### ·*mpfr-2.4.2*

### 如果遇到download_prerequisites里面的地址无法访问 
### 推荐自行下载这些组件到目录gcc-4.9.3/，解压。 
### 然后将download_prerequisites里面的wget全部注释掉，再执行 :
### ./contrib/download_prerequisites

### 做好上面的准备就可以configure了，建议另建一个目录来存放编译文件，默认安装目录是 /usr/local/ 可以使用 –prefix 修改安装路径。
### cd ..
### mkdir gcc-4.9.3-build-temp
### cd gcc-4.9.3-build-temp
### ../gcc-4.9.3/configure --prefix=/data1/gcc-4.9.3 --enable-checking=release --enable-languages=c,c++ --disable-multilib
### make -j4
### make install
### gcc编译编译很慢，一切顺利的话，取决于你的配置40分钟-1个小时后再来看结果吧，我用公司的16核服务器都编译了20分钟

# 第四步
### 配置环境
### export PATH=/data1/gcc-4.9.3/bin:$PATH

### 执行 gcc -v 可以看到下面的信息, 恭喜你成功了!
### gcc -v
#### 使用内建 specs。
#### COLLECT_GCC=gcc
#### COLLECT_LTO_WRAPPER=/usr/local/libexec/gcc/x86_64-unknown-linux-gnu/4.9.3/lto-wrapper
#### 目标：x86_64-unknown-linux-gnu
#### 配置为：../gcc-4.9.3/configure --enable-checking=release --enable-languages=c,c++ --disable-multilib
#### 线程模型：posix
#### gcc 版本 4.9.3 (GCC)
