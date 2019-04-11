# A Runtime Configurable Floating Point Approximate Multiplier for CNNs on IoTs
> Author：Chandan Kumar Jha, Sumit Walia, Gagan Kanojia, Joycee Mekie
## Introdution
### Background
在Iots中，计算消耗大量energy，approximate computing能够reduce energy满足energy-efficient的要求。在IoTs应用较多的CNN中，Floating point multiplications消耗主要的energy，paper提出了一种为low-power IoTs and machine learning applications的Multiplier。
### Problem
现有的Multiplier (eg. CFPU, RMAC) 主要存在的问题：
* the need for a separate exact multiplier (energy consumption)
* unpredictability in error and energy, highly data dependent    
### Solution
提出FPCAM：
* not require the implementation of an exact multiplier
* 根据approximation required，allows user run time configurability
* 在CNNs中compared to exact multiplier具有相似精度，并具有energy benefits
### Result
* 相对于现有multiplier，5× lesser energy
* For ResNet (18 layers) our proposed FPCAM has similar top-1 error and top-5 error as compared to CFPU and RMAC (all use exact multipliers)
## Comments
1. 做对比的两个现有的multiplier分别是在17和18年提出的，作为CNN中基础module，乘法器设计这个topic应该比较热门。作者在浮点乘法器建模的数学推导很清晰，而且这一方法比较巧妙，从而得出的 Architecture 相对比较简单。比如方法中根据乘数的0和1构造的 MUX，只需要一个与门即可实现，而为了调节error的大小，用与门（类似于mask）决定输出是否加入最后的结果。
2. 对energy的估算的方法比较巧妙，根据UMC 65nm technology先设计出1-bit的加法器，提取出energy参数。之后对multipliers建立structural model，通过matlab获取提取出multiplier的所有输入在各个加法器上的transitions来计算总的consumption。这样求出来的结果相对比较精确。
3. paper中没有提到Area方面的Result，面积开销对scalability也比较重要，这一点因素应该是需要考虑的。
4. 结果中对error的研究考虑了最多4-bits Tuning bits，Top-1 Error维持在30%左右。当考虑到更多的位数时，最后的error又会达到什么程度，是更优还是说达到了approximate computing的饱和精确性。这样就可以在面对不同应用场景下在 approximate computing和exact computing做trade-off。
