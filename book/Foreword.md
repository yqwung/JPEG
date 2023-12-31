## 前言

本书使用语言要求：
+ 尽量使用makedown基本语法写作，不到万不得已不用html。

本书目标原则：
1. 尽量将每个概念的知识点介绍到；
2. 表述清楚，无歧义；
3. 通俗易懂；
4. 不重复，不罗嗦；
5. 图文并茂；

材料，要达到以下几个目的：
+ 快速：以最短的时间掌握相关技能。所以：copy/paste要适度。
+ 全面：对相关领域，有全面的讲解。这个全面指的是：对技术的历史、现状和未来，都应该有清晰的认识。
+ 条理：由浅入深、循序渐进
+ 趣味：有趣的历史，通俗易懂的示例
+ 培训材料，需要训练的能力：

文章技巧：
+ 归纳法：总结归纳。
+ 演绎法：深入剖析
+ 比较法：对比分析

为什么要写一篇关于JPEG编码的文章？
这篇文章目的是什么？
目标受众

书中难免有一些和错误，如果你发现笔误、⽆效的链接、⼀些你认为我们遗漏了引⽂的地⽅，代码看起来不优雅，或者解释不清楚的地⽅，请回复我们以帮助读者。如果你发现书中笔误，解释不清楚的地方，甚至错误的信息，请回复我们以帮助更多的读者。语言组织不好的地方，

本书的目标是通过这一本书可以了解学习全面JPEG相关知识。

6. 量化表是64大小的数组，值的范围是[1, 255]；一般编码器有3个量化表，亮度分量Y，色度分量Cb，Cr均有对应的量化表；也有一些编码器只有两个量化表，Y分量一个，Cb与Cr共用一个。
8. 编码过程：
	颜色空间转换，RGB转YCbCr，如果原始图像就是YCbCr格式，则没有此步；
	色度数据（UV分量）下采样；
	零偏置：将原图像素值范围[0-255]减去128，范围变为[-128,127]
	分块（分成8x8像素的块）；
		二次采样后，每个通道必须分成 8×8 块。
		根据色度子采样，这会产生大小为 8×8（4:4:4 – 无子采样）、
		16×8 (4:2:2) 或
		最常见的 16×16 (4: 2:0)。在视频压缩中，MCU 称为宏块
		如果通道的数据不代表整数个块，则编码器必须用某种形式的虚拟数据填充不完整块的剩余区域。
		用固定颜色（例如黑色）填充边缘可能会沿着边界的可见部分产生振铃效应；
		重复边缘像素是减少（但不一定消除）此类伪像的常用技术，也可以应用更复杂的边界填充技术。
	离散余弦变换（DCT）;
	量化（图像质量设置，量化表）；
		由于量化阶段总是会导致信息丢失，因此 JPEG 标准始终是一种有损压缩编解码器。
		量化就是用像素值除以量化表对应的值所得的结果，由于量化表左上角的值较小，右上角的值较大，这样就起到保持低频分量，抑制高频分量的目的
	熵编码（霍夫曼编码）；
		无损压缩
