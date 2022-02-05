
RPi 3 的 CPU 架构是32位的 armv7l，RPi 4 的 CPU 架构是 aarch64。

以下是 Raspberry Pi 3 Model B v1.2 的 CPU 信息：

```Shell
pi@raspberrypi:~ $ lscpu 
Architecture:          armv7l
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    1
Core(s) per socket:    4
Socket(s):             1
Model:                 4
Model name:            ARMv7 Processor rev 4 (v7l)
CPU max MHz:           1200.0000
CPU min MHz:           600.0000
BogoMIPS:              38.40
Flags:                 half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
```

以下是 Raspberry Pi 4 Model B Rev 1.4 的 CPU 信息：

```Shell
pi@raspberrypi:~ $ lscpu
Architecture:        aarch64
Byte Order:          Little Endian
CPU(s):              4
On-line CPU(s) list: 0-3
Thread(s) per core:  1
Core(s) per socket:  4
Socket(s):           1
Vendor ID:           ARM
Model:               3
Model name:          Cortex-A72
Stepping:            r0p3
CPU max MHz:         1500.0000
CPU min MHz:         600.0000
BogoMIPS:            108.00
Flags:               fp asimd evtstrm crc32 cpuid
```

## x86、x86_64

[【CPU】关于x86、x86_64/x64、amd64和arm64/aarch64](https://www.jianshu.com/p/2753c45af9bf)

x86是指Intel的开发的一种32位指令集，从386开始时代开始一直沿用至今，是一种CISC（复杂指令集）。  
所有Intel早期的CPU，AMD早期的CPU都支持这种指令集，Intel官方文档里面称为 `IA-32`。  

x86 CPU 迈向64位的时候，有两种选择：

1. 向下兼容x86。  
2. 重新设计不兼容x86的指令集。  

AMD抢跑了，比Intel率先制造出了商用的兼容x86的CPU，AMD称之为 `AMD64`，抢了64位PC的第一桶金。

Intel选择设计了一种不兼容x86的全新64位指令集，称之为 `IA-64`。
由于是全新设计的CPU，且比AMD晚了一步，没有编译器，也不支持windows，因此IA-64挺惨淡的。
后来不得不在时机落后的情况下也开始支持AMD64指令集，但是换了个名字叫 `x86_64`，表示是x86指令集的64位扩展。

x86、x86_64主要的区别就是32位和64位的问题，x86中只有8个32位通用寄存器，eax,ebx,ecx,edx,ebp,esp,esi,edi。
x86_64把这8个通用寄存器扩展成了64位的，并且比x86增加了若干（8？）个寄存器，同样的MMX寄存器的位数和数量也进行了扩展。

## 什么是aarch64

[【arm】系统架构AArch64简介](https://blog.csdn.net/rd_w_csdn/article/details/53841018)

AArch64是ARMv8 架构的一种执行状态。

AArch64 不是一个单纯的 32 位 ARM 构架扩展，而是 ARMv8 内全新的构架，完全使用全新的 A64 指令集。这些都源自于多年对现代构架设计的深入研究。更重要的是， AArch64 作为一个分离出的执行状态，意味着一些未来的处理器可能不支持旧的 AArch32 执行状态。 虽然最初的 64 位 ARM 处理器将会完全向后兼容，但我们大胆且前瞻性地将 AArch64 作为在 ARMv8 处理器中唯一的执行状态。我们在这些系统中将不支持 32 位执行状态， 这将使许多有益的实现得到权衡，如默认情况下，使用一个较大的 64K 大小的页面，并会使得纯净的 64 位 ARM 服务器系统不受遗留代码的影响。立即进行这种划分是很重要的，因为有可能在未来几年内将出现仅支持 64 位的服务器系统。没有必要在新的 64 位架构中去实现一个完整的 32 位流水线，这将会提高未来 ARM 服务器系统的能效。

AArch64 作为在 Fedora ARM 项目中被支持的 ARM 构架是一个很自然的过程： armv5tel、armv7hl、aarch64。新的架构被命名为 `aarch64`，这同 ARM 自己选择的主线命名方式保持一致，同时也考虑到了 ARM 架构名与 ARM 商标分开的期望。

ARMv8-A 将 64 位架构支持引入 ARM 架构中，其中包括：

- 64 位通用寄存器、SP（堆栈指针）和 PC（程序计数器）  
- 64 位数据处理和扩展的虚拟寻址  

两种主要执行状态：

- AArch64 - 64 位执行状态，包括该状态的异常模型、内存模型、程序员模型和指令集支持  
- AArch32 — 32 位执行状态，包括该状态的异常模型、内存模型、程序员模型和指令集支持  

这些执行状态支持三个主要指令集

- A32（或 ARM）：32 位固定长度指令集，通过不同架构变体增强部分 32 位架构执行环境现在称为 AArch32。  
- T32 (Thumb) 是以 16 位固定长度指令集的形式引入的，随后在引入 Thumb-2 技术时增强为 16 位和 32 位混合长度指令集。部分 32 位架构执行环境现在称为 AArch32。
- A64：提供与 ARM 和 Thumb 指令集类似功能的 32 位固定长度指令集。随 ARMv8-A 一起引入，它是一种 AArch64 指令集。

ARM ISA 不断改进，以满足前沿应用程序开发人员日益增长的要求，同时保留了必要的向后兼容性，以保护软件开发投资。在 ARMv8-A 中，对 A32 和 T32 进行了一些增补，以保持与 A64 指令集一致。
