# llvm6.0-simpler-install
llvm6.0 simpler install steps on Ubuntu16.04
通过百度网盘分享的文件：llvm6.0.0
链接：https://pan.baidu.com/s/1f1XltQJuThjKiK60o5Tmzg?pwd=ih74 
提取码：ih74
# Linux环境下LLVM 6.0 + clang安装步骤

本文详细介绍了在Linux环境下安装LLVM 6.0和clang的步骤。LLVM是一个开源的编译器基础设施项目，而clang是LLVM项目中的一个C语言家族前端。通过本文的指导，您将能够在Linux系统上成功安装并配置LLVM和clang。

## 准备工作

1. **确保系统联网**：在安装之前，请确保您的Linux系统已经联网。参考作者使用的是在Windows 10环境下通过VMware 15虚拟机安装的CentOS 7系统。本人使用的是WSL2下的Ubuntu16.04（对于这种19年的老项目有更好的兼容性）。

2. **下载所需tar包**：安装过程需要三个tar包，分别是clang的源码包、动态测试工具包和LLVM的源码包。您可以从官网下载这些包，或者从提供的百度云链接下载。

## 安装步骤

### 1. 解压LLVM源码包

在root权限的根目录下创建一个名为`llvmtest`的目录，并将LLVM源码包移动到该目录下。使用以下命令解压文件并重命名为`llvm`：

```bash
tar -xvf llvm-6.0.0.src.tar
mv llvm-6.0.0.src llvm
```

### 2. 解压clang源码包

在解压后的`llvm`目录下有一个`tools`目录，将clang源码包移动到该目录下并解压，然后重命名为`clang`：

```bash
tar -xvf cfe-6.0.0.src.tar.xz
mv cfe-6.0.0.src clang
```

### 3. 解压compiler-rt源码包

在解压后的`llvm`目录下有一个`projects`目录，将compiler-rt源码包移动到该目录下并解压，然后重命名为`compiler-rt`：

```bash
tar -xvf compiler-rt-6.0.0.src.tar.xz
mv compiler-rt-6.0.0.src compiler-rt
```

### 4. 编译安装

确保您的Linux系统中已经安装了cmake。如果没有安装，请先安装cmake。然后，在解压后的`llvm`目录下新建一个名为`llvm-build`的目录，并进入该目录进行编译：

```bash
cmake -G "Unix Makefiles" -DLLVM_ENABLE_ASSERTIONS=On -DCMAKE_BUILD_TYPE=Release ../llvm
make install
```
cmake -G "Unix Makefiles" -DLLVM_ENABLE_ASSERTIONS=On -DCMAKE_BUILD_TYPE=Release ~/llvmtest/llvm

（EricWang1358注释）如果安装它的流程，llvm文件夹并非在根目录下，而是在llvm文件夹中，所以需要调整路径。同时，在此步骤前，确保cmake 和 essentials已经安装到16.04虚拟机中。20.04由于gcc版本过新，make时会出现找不到ustat包等情况，这也是为什么重新下载ubuntu16.04这一16年发行的虚拟机版本的原因）

编译过程可能需要两三个小时，请耐心等待。
（EricWang1358注释）现在的高性能电脑使用 make -j6 或者 make -j8可以在十分钟以内编译完成。


### 5. 环境检测

编译安装完成后，可以通过以下命令检查环境是否安装成功：

```bash
llvm-config --version
clang --version
```

### 6. 用例测试

编写一个简单的C语言程序，使用clang进行编译。例如，编写一个名为`hello.c`的程序，内容如下：

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

使用以下命令进行编译：

```bash
clang hello.c -o hello
./hello
```

如果程序成功运行并输出`Hello, World!`，则说明安装成功。

## 总结

通过以上步骤，您已经成功在Linux环境下安装并配置了LLVM 6.0和clang。希望本文对您有所帮助！
