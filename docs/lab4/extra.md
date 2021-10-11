# 附加题

- 如图1-17所示，必做题CNN的预测准确度是95.13%。基于此，本题要求：

    （1）对CNN模型进行优化，以提高模型预测的准确率；

    （2）优化卷积和池化IP核，以提高CNN硬件加速器的性能；

    （3）列表对比优化前后加速器的前向推导性能差别，并计算加速比（$ Speedup = T_{origin} / T_{optimized} $）。

- 本题不作硬性要求，学有余力的同学可自行完成。

## 1. 网络参数格式转换

- 利用虚拟机中的~/tensorflow/dat2bin工具，可将.dat格式的网络参数转换为.bin格式。dat2bin工具的使用方法如图2-1所示。

<center><img src="../assets/2-1.png" width = 500></center>
<center>图2-1 data2bin工具使用方法</center>

## 2. 优化方法参考

- 对于卷积和池化运算，可以尝试从局部性和硬件并行性的角度展开优化。

- 以下提供4个优化思路作为参考：

    （1）局部性原理：在卷积和池化操作中，存在多重嵌套循环，请分析如何调整循环结构以充分利用数据存储的局部性；

    （2）数组划分：分析卷积和池化的输入输出接口，使用HLS directive中的Array Partition来完成数组划分，该pragma的具体语法请参考Xilinx官方文档；

    （3）循环展开：可以考虑使用#pragma UNROLL来优化加速器，具体语法请参考[Xilinx官方文档](https://www.xilinx.com/html_docs/xilinx2017_4/sdaccel_doc/okr1504034364623.html)；

    （4）流水线优化：可以考虑使用#pragma PIPELINE来优化加速器，具体语法请参考Xilinx官方文档。
