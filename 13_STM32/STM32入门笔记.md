# 1.EXTI外部中断

##  中断概念

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTc4MjQxYjRkMTdlN2ZkMzg2ZjJlZjRlOTA0OGU2NzBfdllUbGpudzZiR3FaR3dYV0tacml2R0pUcjBJTnllZ0xfVG9rZW46R1NNNmJzeGZEb3JzRE54MUVya2NlelQzbm9mXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

总结：当中断满足的时候，CPU暂停运行，进入中断执行相应逻辑

 

##  中断执行流程

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjkwOTFmMmVhMGNhMjkyYWI3ZDE2MDc0ZDQwOTgwN2FfZXdlTGVxbGJ3UldScjFQZ2VNU2tmaW9Mc1RmZEhvV3BfVG9rZW46SWxNbmJoZ0d4bzJaV0V4WVhKaGNZVnRybmVkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

中断优先级：根据多个中断的紧急程度，进行顺序执行

 

中断嵌套：中断内部嵌套中断，当执行一级中断的时候，如果再次触发内部中断，就会进入二级中断 执行逻辑： 主程序->一级中断->二级中断 执行完成后 二级中断->一级中断->主程序 继续运行

 

 概念：

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YWZiYThjZmQ1NWYyMjU4OWQ3Yjc1Y2UwODVjMzJiZTFfMjBTbEhza2dpa3JNWEhqOUFLUTlvNzB5Nm95U0NqcUlfVG9rZW46SkpWYWI1bTlCb3l3eDh4V0N4MWNpR0QybnpmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

 

## 内部外设中断：

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDg5M2ExMjc0MzJjOWJhMGU0MDljNTg1MTgxMGI5MmVfeFBtSFdIRlpXQ3NKR2Y2VmhPVVJhbDZhenBGVWhudGNfVG9rZW46VnVUcGJWaVVIb21pdDJ4c3RGR2Nsa29wblJmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 中断响应跟事件响应的关系与区别

事件相应不会触发中断，而是触发别的外设的中断操作，属于与外设的联合工作，而中断响应属于正常流程，引脚电平变化触发中断。

## **1.NVIC**

**Nested Vectored Interrupt Controller的缩写，即嵌套向量中断控制器。**

在STM32等微控制器中，NVIC用于管理中断，它可以实现中断的优先级设置、中断的使能和禁用、中断的嵌套等功能。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDYwOWUwZDgyZDZiYWZkODA3OWRjYzU4YjgzNWVmOGZfR3RYVkNqZWhSYXh4a2g2eERFZ2JaeXdtTXMwOWN5THVfVG9rZW46TWpPYWJFajg2b0tDMlp4SlIzeGNRb0FybmNmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### NVIC优先级分组

以医院排号为例，响应优先级可以插队看病，我没有取了最后一个号，但是等上一个病人看完病，不管排了多少人，我都可以先看病 。 抢占优先级可以不等上一个病人看完，直接叫号进行看病，抢占优先级高的就可以进行中断嵌套。两个中断的抢占优先级跟响应优先级都一样的，以中断号为排序。数字越小优先级越高

解释：四位寄存器 即为 0000

如果抢占优先级0位，取值为0 那么到1111 就有时16种情况

如果抢占优先级1位，那么高位置只有0跟1 两种选择 ， 而000对应0 111对应4+2+1 =7，所以相应优先级有8种选择，而抢占优先级有2 种选择  ，数字越小优先级越高。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTg1MjY3NmUwNzFiN2I1YmY2NmFkODMyNzcyOWM4YmJfVTVPR1paaUU4c3N0b2N5SE1GWWVEbHpiaGVKVnpiNnBfVG9rZW46VW5xd2JVbENjb2t6Tmp4V2tmMWNlQUNEbnRiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### NVIC 的基本结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjE3N2NiNjY0OWRiYTFmYmMzNzc3YmNhNGQ3MzIzYzlfZmlWRW9NOEhyVGQySXkyQXdjQUNGSXFBQm0wa09FMXBfVG9rZW46UHNmdmIyZmwxb0U1NjR4d21hQWNlSjAzbmVkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

CPU 为医生，NVIC 为叫号系统，会可以优先安排紧急的病人；

## 2.**APIO中断引脚选择器**

他可以在三个GPIO的16个引脚里面选择一个进入EXTI通道

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTI3OWEwOGFjMWRkYjRiMTY4MDVmOGIyYTZlOGIwMWRfcE9BTmR3ZWRyZkNKUkVzZGVyNU1XR0hqb1JtZFpiNk5fVG9rZW46WlpJa2J0UHJYbzZyT0l4Smk5TGNCWXVrbkRoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

**APIO 主要有两个功能，第一个就是刚刚讲到的中断引脚选择，第二个就是引脚重映射，这里补充一下引脚重映射的概念。**

### 引脚重映射：

是指将特定外设功能的引脚重新分配到不同的引脚上，以满足不同的硬件设计需求和提高系统的灵活性。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzU0YTFkMDIzOTUwN2NjN2QyZjljM2EwMjdhNWU3Mzdfb0dLM0I3VkVhSXRHTmsxeWNhTURMOE5td3BDbGlmNW9fVG9rZW46UkZMOWJrdkxIb1FxZkJ4d1c1RGNRMTVxbm5mXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 3.**EXTI**

（External Interrupt/Event Controller，外部中断/事件控制器）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzMwNGMzMGY0NjQ1OWM4OWNhOGJiZTA2YTQ4YWU1ZDVfb1NYelBCTE1ES0tQRUowS2lvV0EzSHF0YmxKejZYcTNfVG9rZW46VzB0dGJ1YUxLb1B1YW54VU12SWN6Q3VmbmZkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 总结：引脚电平变化，触发中断，软件触发：程序触发，支持所有的GPIO口，**但是Pin号相同的，不能同时触发中断。**

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmVkOGY5ZWZkNTYyNGRhOTFhOTA1Y2I2NTMzZDcyOTJfR2g2azhJeGRTTmJaNkdPVlBVeE5ncEdPdjh1ZDJ3MEpfVG9rZW46SU03RGJDZTlpbzd6SWJ4RlFXcWNJdEQ5bk1iXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

这里的输入线，就是20根输入线 ——> 边沿检测电路 上升沿触发寄存器跟下降沿寄存器可以选择触发方式——>或门输入端

### 逻辑符号说明：

1.   或门： 长得像导弹头（可以有多个输入，但是只能有一个输出），只有全部输入0 输出才为0
2.   与门：大于半圆（同样有多个输入，但是只有一个输出，只要有一个为0，那么输出就为0，只有全部为1 才会为1）
3.   非门： 三角形，一个输入输出，输入0 就为1 输出1 就为0
4.   数据选择器，符号为梯形，有多个输入，一个输出，侧面有选择控制端，根据控制端数据，从输入选择一个到输出，这些就是常见的逻辑符号
   1. ![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjM1ZmUxZDQ2ZWM2YWI3M2Y2N2ZiNWQ3YmNmMTYzNTNfTXBoRTJmV0k1QjJsb25NWGFDVUxHT2lKQUJxUld6aXNfVG9rZW46VE54Y2JhQjNZb0tpMHd4dHVBeGNEdjZrbktmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTZhYWY1MjQzMWUxMGZkMmEwNDBmZDlhZWVhOTk3ZTVfV3pDNFdHRVZYaVF2UFJZV1lEc0NoVWhWMUtoRUlLZ1FfVG9rZW46SDRScmJVSm9CbzhvQW94ZVhHTWMwWUlzbkRoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)
   2. 
   3. 

总结，当面对突发事件的时候，可以用到外部中断

# 1.1旋转编码器

## 旋转编码器概述：

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjdhYjliYzg3OTVlYTEwMjc2YzFiN2YzMDc5ZDEwNTlfZEJZdjQyaVpOTFAzb210Z0ZvMElpYmJJUVZ3UWlSU1ZfVG9rZW46WTR1VmJGbzQzb1UyRkZ4MTN4QWNQN05LbnpjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 1.光栅编码器

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjFkY2Q0MGM5N2YyZmJjNWJiYTZmZjhiYWYxMDc4ZThfQkh1U2dlVTlJZTF0QThTa2p2dGY5MEl6djdpZFdUbnNfVG9rZW46VHo2VGJheE9Jb2VUcEl4UW9EeWN2Y2x4bkVRXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

光栅编码器是一种利用光栅的光学特性来精确测量位移的装置。它由主光栅和指示光栅组成，物体移动使透过光栅的光发生变化，经光电探测器转换为电信号，通过计数脉冲确定位移量。具有高精度、高可靠性和快速响应等特点，广泛应用于工业和仪器仪表领域。

然而，光栅编码器存在一些不足。它只能计算位置和速度，不能判断方向。在某些应用中，这可能会限制其使用。为了弥补这一缺陷，可以结合其他能够判断方向的旋转编码器，以提高测量的准确性和全面性。

### 2.旋转编码器

旋转编码器是一种用于测量旋转角度或位置的传感器。它通常由一个旋转轴和一个固定的外壳组成，内部包含了光学或磁性的编码元件。

旋转编码器可以产生正交波形，也称为 A 相和 B 相波形。这两个波形具有以下特点：

#### **一、波形特征**

1. 相位差：
   1. A 相和 B 相波形之间存在 90 度的相位差。这意味着当旋转编码器的轴旋转时，A 相和 B 相波形的上升沿和下降沿会交替出现，且相位相差四分之一周期。（见图2）
   2. 例如，当 A 相波形处于高电平时，B 相波形可能处于上升沿、下降沿或低电平状态，具体取决于旋转方向和编码器的分辨率。
2. 脉冲数：
   1. 旋转编码器每旋转一圈，会产生一定数量的脉冲。这个脉冲数通常与编码器的分辨率有关。例如，一个分辨率为 1024 线的编码器，每旋转一圈会产生 1024 个脉冲。
   2. A 相和 B 相波形的脉冲数是相同的，它们可以用来确定旋转的角度或位置。通过计数 A 相或 B 相波形的脉冲数，并结合相位差信息，可以确定旋转的方向。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjZhMzJmYzJhMTMwMTYwNTZjOWQ0MjYzNzBiYjUwYTZfR3hESDk3OXhCTUppMVp0WXI2T3NaaVZFVkVrZGgwZjRfVG9rZW46RW5qTWIyRVh2b3AxbmJ4aW0yR2N3NFRSbktiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDE4ZmQ0M2UwNjEzZTQyMDVjNTM2NTE0YTQ4M2I0NGNfZmJQamFZNDJRU0YzaGl0SzllWFlBUXRXYk5WdmdxUzhfVG9rZW46VERMdmJEUnR2b1d3akZ4eFV1VmN4REdyblZiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

​                  正交波形 图2

###  3.霍尔传感器编码器

**一、工作原理**

霍尔传感器编码器通常由一个磁体和多个霍尔元件组成。当磁体与霍尔元件之间发生相对运动时，霍尔元件会检测到磁场的变化，并产生相应的电信号。这些电信号可以被处理和解读，以确定旋转角度、线性位移或速度等参数。

**二、特点**

1. 非接触式测量：霍尔传感器编码器采用非接触式测量方式，不会对被测物体产生磨损，具有较高的可靠性和寿命。
2. 高精度：能够提供高精度的测量结果，适用于对测量精度要求较高的场合。
3. 快速响应：对运动的响应速度快，能够实时监测被测物体的运动状态。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODA3YjAyY2U0MmFkZTNmMmM3OGQxOTJhMzBkMjkxNmNfZGFEYU9FOHJsMHR1cUFhQ3Mya2FFSFdTZVRGc1VKeHJfVG9rZW46S2V1a2I2VDFPb1FFdjd4bVROQWNraDJtbkxmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 4.独立编码器元件

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YmM3MGVhYTZjYTY0OGEzMDFjZWRmNDdlZjBhZTE4NmFfRlI4dTJVMUl4R0pheXVjU1hTTWdwalVHNTlnMFNXVFpfVG9rZW46WndZTmJwREVvb0liV214WFdHQmMwZko2bkpkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

独立编码器元件是一种可以独立工作的用于测量角度、位置、速度等物理量的电子元件。

**一、结构组成**

通常包括码盘（可以是光学码盘、磁性码盘等）、检测元件（如光电二极管、霍尔元件等）以及信号处理电路等部分。

输入轴转动，输出轴就会有波形。

## 旋转编码器硬件电路

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTY3MTA4ZWFjZjExM2U4ZTMwMTYwNzdmOTUzZWY2NzNfUE0yWGozZHRQeU1YekxGSE82SFRldlBxN0hDd0xCMFdfVG9rZW46WW9wRmJKeHczb21vcnh4eVZYQmNXcDJmbkhjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 编码器控制数值 代码实现

暂时无法在飞书文档外展示此内容

### 硬件电路接线

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjY1ODE1ZDZmYzFkYjAxNTgxMzNjYmE4NmEwZTAxYjNfUXJOWkg2QjdNYnVuZ0Q0eEdMUnNiTTlnY01JdkVxbHRfVG9rZW46QVh1cWI4ZjdsbzV0c0t4c0FVdGNxeHAwbnBoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 初始化代码

暂时无法在飞书文档外展示此内容

### 主程序

暂时无法在飞书文档外展示此内容

### 实现效果

旋转编码器正转的时候数值增大，反之减小，另外这款编码器的sw 口（switch）还可以在按下的时候作为按键使用，有兴趣可以自行研究

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGE5YWQzZjRjNThhYjVhMTc3NjQ0Y2JhMWI2ZjFhZDFfbzVjWE5UTTNybUEydEVIeGd3a1oxRW9jU2duSmJRQm9fVG9rZW46RkpsaWI0MU55bzBnRXZ4bDM4R2M2Wk1kbjBnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# 2.TIM定时器

### TIM概念

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2ZlZTVmMTg4N2E1NjZlMWU1OWUyZGU4Y2Q3NDVjNGVfYmxTWDNmdmhYSHFISVBjZ3VSbDROQktPZHYyYkpwcjBfVG9rZW46R2F1VmJzWjFHbzZMMkV4SkgxQmM4Z0RublpiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

16位计数器：仓库的概念每来一个时钟信号 ，计数器➕1

预分频器：可以对计数器的时钟进行分频，让计数更加灵活

自动重装寄存器：设定触发，让计数达到一定数值的时候，进行中断的申请

总结：三部分统称为时基单元，并且都是16位的寄存器，那么最大数值2的16次方，也就是所有数值最大设置，就能实现59.65秒的定时 72MHz / 65536 / 65536 得到中断频率，取倒数就是最大定时时间

最大定时 = （最大计数器）*（最大自动重装数）/72/Mhz

## 定时器类型

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjZmMDE2M2YwZTRjOGNhMTIwYjUxOTY1OGM3ODgyNzJfeG1JZ1VIS2NqdTZzZ1RmVmJQUlg0cWcwQVYybDBRNW9fVG9rZW46TE1lTWJVbUdTb2dmeGp4NmNta2NlcmVPbnFkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 基本定时器

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTIzMzM0MzVmZWExYzAyNTk3M2IzMWVhOWM0ZGFlMTFfbExQWXJoM09IbmltMjBkSWhlclJ2dTR1d2VRaktZNjVfVG9rZW46UVhPbmJhNDNzb1dKb3p4QmFQNGMzRkRibkVnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 主从模式触发DAC 的功能

DAC即数模转换器（Digital to Analog Converter）

当需要用DAC 输出一段波形的时候（例如PWM），那么就需要每隔一段事件来触发一次DAC，让他输出下一个电压点，如果用正常的更新中断来手动触发DAC 转换的话，就会极大占用资源，影响主程序的运行和其他中断的相应，而在使用主模式下，可以将触发事件映射到触发输出TROG（Trigger Out）的位置然后TRGO就直接接到DAC 这样定时器的更新就不需要经过NVIC 中断响应来触发DAC转换了，过程不需要软件的参与，实现了硬件的自动化。

注：D是数字两 A是模拟量

暂时无法在飞书文档外展示此内容

### 通用定时器

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjU1YmJkNTIzNTQ5Y2M5ZThlMDNmOWI3YTBiNjMzNWFfcWVpSjAyUWFuSTBmVGRyNEN5bWFsbUdOSG9YUmVlOW5fVG9rZW46Vzd2U2JtUVZobzR0dDJ4TUxLdWNENklibnZoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

向上计数： 计数器从0开始向上自增，达到设定值，清零同时申请中断，依次循环

通用/高级定时器除此还支持乡下计数以及中央对齐计数模式；

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2FkYzM1MmY1OTQ3MjU1Zjk2OGFmY2Q0ZDVmODg0MTVfaThPZ3VOQWg4QjQyRlhpNmcySFRxOHQ4VEhhRGhidlVfVG9rZW46VXFEcWJ3UUhabzQ0SGF4YXB5ZmNKcnc2blNnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

情况1 

暂时无法在飞书文档外展示此内容

情况2

暂时无法在飞书文档外展示此内容

情况3

暂时无法在飞书文档外展示此内容

总结，外部时钟模式1 下，输入可以是ETR引脚。其他定时器，CH1 引脚的边沿，CH1 和CH2 引脚，一般情况下，使用ETR 为外部时钟输入

**输入捕获电路/输出比较电路 （之后会详细介绍）**

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MGFlYWIxNzQ5M2JlMWNiNmNiNmE5NzMxZTU1Y2RjNGZfdzJpSklwOEJ1WlVodjBka2p3RXQ2Y1lOVGZLbWFWbjlfVG9rZW46Umg3YWJKbmRzbzJldTB4WnJnb2NTTFc0bnJiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

输出比较电路有四个通道分别对应CH1 到 CH4的引脚，可以用于输出PWM 波形

输入捕获电路也有四个通道，可以用于输入方波的频率测量等

中间的是输入捕获跟输出比较电路寄存器，两个电路共用四根引脚，不能同时进行

### 高级定时器

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjEzMWMzYzNkMzBkNWI5OWYxNGUzZDNlMDBjM2NmY2NfTVZXRDJzWE0yVHNOU054TVRzRVFVYkFoUjNTejFRcmVfVG9rZW46RTdNY2JkNXRub3dKeWN4TEpyS2NUcEljbjNjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

相比于通用计时器，这里首先在申请中断的地方 增加了一个重复次数计数器，可以实现每隔几个计数周期，才发生一次更新事件和更新中断，这就相当于对于输出的更新信号，又做了一次分频，这里可以实现级联计时器的效果。

DTG （Dead Time Generate）死区生成电路   防止桥臂直通现象

BRK 刹车输入功能 如果外部BKIN产生刹车信号，或者内部时钟信号产生问题，那么就会自动切断电机的驱动，防止意外的发生

## 定时器中断基本结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWIwMjZjZmUxOTJlNzg2MDRlYzU0NjE5YmZlMzE3N2RfN3VqQ0tNQXJEUEtuNTJJSVk1T2JRU0V1Y0tYaURkZHFfVG9rZW46SGs4WGJ0dGhTb3dpVUR4THJzNGNudVRIbnBoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

运行控制：控制寄存器位的，比如向上计数，向下计数，启动停止等等

中断输出控制：中断输出允许位，如果需要中断，就允许

暂时无法在飞书文档外展示此内容

### 预分频器时序

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDRmN2ExNmY2NzAyMWMxZDhiMWQ5OGQxMDg4ODUwYzJfbjVYTmtGYXR4d3R6c0hDNmhiQzNPZmJEVUZkTWk5YmJfVG9rZW46RHlmQWJZT1BZbzYzNjV4TmpBR2NhYUUwblpjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

 CK_PSC 时钟源;  CNT_EN 计数器使能； CK_CNT 计数器时钟，他即是预分频器的时钟输出，也是计数器的时钟输入

 缓冲寄存器（影子寄存器）:在计数过程中，如果突然改变分频数值，只有等到更新事件后，改变后的分频数值才会真正生效

 计数器计数频率 = 时钟源频率/（分频器数值+1）；

###  计数器时序

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTIyMzY3ZTJiODgxY2IzNTllODZiYjJiMDVmNWQxOGFfS3BGazM0SUdVR3RaQ3NGNlBSckg1R3pqeFhUZFliU3pfVG9rZW46UllzTWJaYVhJb0xoV2h4elJTTGNoM0dRbk5jXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

计数器溢出频率=时钟频率/（设定定时阈值+1） | =定时器时钟源 / （分频系数+1）/（自动重转器系数+1）

注： CK_CNT 跟 CK_PSC  虽然同为时钟，但是CK_PSC 为时钟源，SK_CNT 为预分配器的输出，也为CNT 计数器的输入，是经过处理后的时钟，

定义：计数器溢出频率是指一段时间内，有多少个计数周期，与其呈反比，计数周期越短，溢出频率（触发频率）也就越大   溢出时间为溢出频率的倒数，例如溢出频率为10MHz 表示1秒内，会发生10次的溢出，那么每次就为1/10

### 计数器预装时序

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzBhNWE3ZTFhMzUxMjA2MDBiYWVkY2IwYWY1NWUxMjdfZ21RNUl2aUhmTGd2RlNZSTBqVUI0V091VXZjMnZOd3JfVG9rZW46TUI1R2JjREROb05ubHN4U0hyNGNlYnJYbm0zXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDQyNzhlYzk5OWM1OTYwMTg1YTNhN2FiM2NhOWJmODRfellzUEZSRlZ4eVU0VURubEpnSDZrclZicFVKNmF3dkJfVG9rZW46SUJCOGJZc3lBb3BkM1Z4NFpiVWM5RUtKbjNiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

让数值的更改与更新事件同步发生，防止运行途中出现错误，通过第ARPE进行设置就可以开启/关闭

## RCC时钟树

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDMyNzcwMTMzYTAwOWNhNzU3YTRkZmNiMTJlYzc0YzRfUjJ1dk5admtOeTVHeUZTa1VyQWI3V2JGd3ZhWEJpeGJfVG9rZW46R1NtbGJZbTV4b3lNTzl4UUtJZmNpazFTbk1nXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

主要分为时钟的产生电路与时钟的分配电路两大部分

### 时钟产生电路

在时钟的产生部分，有四个震荡源，高速晶振提供系统时钟AHB APB2 APB1 都是来源这两个高速晶振，外部晶振比RC 内部振荡器更稳定准确

内部的8MHz高速RC振荡器 

外部的4-16MHz石英晶体振荡器，也就是晶振，一般都是接8MHz

外部的32.768Khz低速晶振，一般是给RTC提供时钟的  RTC（Real-Time Clock）即实时时钟

内部的40KHz低速RC振荡器，这个可以给看门狗提供时钟

暂时无法在飞书文档外展示此内容

CSS （Clock Security System） 时钟安全系统

一旦外部时钟失效，就会让内部RC振荡器作为时钟

### 时钟分配电路

所有定时器时钟频率都为72MHz 

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWI3YTE1OTBjNWFiNTQ4ZDgwZGRhMjQ5ZTg0YWIwMDVfWFIwQ3VGREhGeGxLdEM1QjdXdnc4S1N5VjJCTmprZk9fVG9rZW46RXRYN2JvWmhmb0NVRkp4WlpQdGM5cndvbmVoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 定时器定时中断（代码函数部分）

硬件连接

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODcwMTg0ZDgwOWZmYjZlYzQ0NzQ3YWNkOTFmYTI2ZTRfSGlPc0ZpcFRSRThybkg4Sk85ZW5JRnhUT0t0RVVtUGZfVG9rZW46STVQb2JjUnBnb2VUOWh4dmNra2NTN0xGbnpjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

根据定时中断基本结构进行配置

暂时无法在飞书文档外展示此内容

### 相关配置函数列表

暂时无法在飞书文档外展示此内容

### 用于中途单独更改设定数值的函数：

暂时无法在飞书文档外展示此内容

### 初始化函数部分

暂时无法在飞书文档外展示此内容

### 主函数main

暂时无法在飞书文档外展示此内容

代码效果，实现Num变量每秒自增+1

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDQyNmQ0ZGYzZTM1OGU5MDQzZDdkYTcyY2U3NzNjNWFfVHFmc01JYmdyTVQ1TGVQa243ZGoxWGs1d2V1anlXN3NfVG9rZW46R1BtdGJpb0Q1bzBPeGx4dFJYb2N0aWkwbnNlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

但是这里有一个现象不知道大家发现没有，就是stm32每次复位，Num的数值都会直接变成1 ，按理来说，应该以Num 的初始值0开始的，这就表明，在初始化的时候，程序就进入了一次中断，要解决其实也很简单，这题就出现在了这里

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjEzNDYyMmZmZTAwY2U0ODJhOWU2MTUxMzFmZjExODBfMXQ1OUhYREhOS1ZQV3VDaEhIRTcwa1lZOFNNQ1p6QjNfVG9rZW46TjFyOWJ2QmVrb285Tk94SjNENmNCaFJNbkxoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGI4NTZlNTlhOWMyZTUxNTk3N2UzZGM5YTE3MjkwZjJfVmZKc1FSTmR0alBTNU9JZldsTURRWG94MmhKdzhRbXpfVG9rZW46VjNKNGJxTWJrb202ZlF4UVRQcWNqS1d2bk9kXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

这个的意思是生成一个更新事件以立即重新加载预分频器和重复计数器的值，要知道，我们的预分屏器是有缓冲寄存器的，我们写的值只有在更新事件的时候，才会有效，这里为了让数值在初始化的时候生效就生成了一个更新事件，缺点就是更新事件与更新中断会同时发生，导致以上电就会从1 开始计时，想要解决其实也很简单

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDZiMWY4NmI5OTI2NzIyMDQ1MGZmMzU4ZDg2MWI5ODdfcHlwNzhJNnloOEk0Vk9BdkpWM1poSlFQaDV2cTlRR1NfVG9rZW46QmZpaWJ6akZwbzViRUx4ZmxlbGNzcTl4bnBjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

现在就可以正常显示啦！还可以在主循环里添加查看计数器数值的代码，可以发现，从0到重装值10000后，才会发生一次更新中断

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDAxY2MyOTc3N2ZiOTMxODhiYTJhN2E5NzkwNTY4ZmFfb3FweXY0M0Y0TmJ2MThpNEZMc2pWd3VJZDJzdGRaMWpfVG9rZW46Sjk3QWJvOEdIb1BGZDJ4cGl6cGNvZ1dQbnRkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTk0MzRmYzRiZDBhZTA2Mzc0NjhhNTJkYzJjMDc4MGZfVzhSV3I5VXhLaG1heFNrUFluMlh5Qk85ZklhMEJOV3VfVG9rZW46TWNFOWJvdndrb1hZQ1Z4VHp1SGMyNk9abjRmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

外部时钟模式2函数，可将时钟源选择为外部引脚输入时钟

暂时无法在飞书文档外展示此内容

# 2.１TIM 输出比较

### 输出比较介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmM1ZGRjZmI1OWFkMjYxMzNjYTJkOGNmZTViODg4YTNfSW85SFRyUUxnUGhXOXdiNFpOQ0hUR1k4VlNYdGwzUXBfVG9rZW46WmZNMmJVSldvb250ZUd4Yk1HNmNwVllhbkJlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmJiMzliYzZlNGRhZDFhNzk2MjJkNjg2NjVmZGFlYTNfR25ibmFCa3lFVkRiVlY2b2ZxQklSS253R1pQZXM2WEFfVG9rZW46T280VWJMcWVRb3ZrblR4SHpNd2NYR1lMbk5iXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

这是是CCR捕获/比较寄存器，是我们给我给定的一个数值，当CNT计数器的计数数值，大于，小于或者是等于 CCR 的值的时候，这里的输出就会对应的置1 置0 置1 置0 形成一个PWM波形。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTk2Y2E5NjUxZWRhN2ZiOGI0Njg5OWUwNmEwNjRlNDZfQmNoUlJiNmlYWnJna1d6b2txNkVsSUhMUERiVnFHN3lfVG9rZW46TUdnYWJScDI1bzNKRHJ4YVdMUmNLd1pNbnVlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### PWM简单介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OWVlODUyMmUxMGE5NWYxY2E4ZWQ0NzRkNTQ2MjM2NTRfUVhodFNHY3F1Z1dGZWhLNXBZeEJETjhjYlFxV3hicW5fVG9rZW46QXViNWIzQk1jb2lrM0N4U2h0RWNzNGZyblExXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 频率 ：一秒的时间内，出现周期的次数，就是频率 所以 1/Ts

#### 占空比 ：高电平时间占整个周期的比例 ，例如 占空比20% 那么就是高电平20% 低电平80% ，占空比决定了等效的模拟电压，占空比越大，那么等效的模拟电压就越趋近于高电平。反之趋近于低电平，例如：如果高电平是5V

#### 低电平是0V 那么在占空比50%的情况下等效2.5V 20的占空比就等效于，1/5处的电压，就是1V

#### 分辨率：分辨率是指输出的电压梯度，而频率是指输出变化的次数

处暑比较通道（高级）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmQxNjIwODNhY2QyNjJlNjQ5MWI1NTg5NzQ4OTUyMDlfMzlWMGUwRnRUS1Q0WEhITnhOZDZZYTBCcWk3Rm1MUEhfVG9rZW46RWNKWGJGaWJYb2tiWXJ4aTlwY2NqV2JibkhkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

这里首先对于CNT跟CCR进行比较，当CCR大于或者等于CNT 的时候，就会给输出控制器一个信号，然后就会改变他OC1REF 的高低电平 REF（refernce） 意思就是参考信号，接着就会进入极性反转电路部分，这里如果CC1P为1 那么输入多少就会输出多少，如果置1 那么非门就会将信号反转输出。

### 输出比较模式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDIxOTlhYjk3NGZlNjY3MWMyMDMwMjk5MTFhNWE4MWZfTGhhODBSZld1NkpYTGg3NkxrRUdmZGJGSTlMd1FPQkhfVG9rZW46QjBkN2JHSUFmbzNjNHZ4V1FJUGMwazdEbkdlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

冻结： CNT跟CCR无效，REF保持原来的状态，不管CNT的大小，REF保持上一种的模式，当你正在输出PWM 波形，但是想暂停一会儿的时候，就可以用到它，一进入冻结模式，输出就会停止了

匹配时置有效电平：置高电平

匹配时置无效电平：置低电平

匹配时电平翻转：可以用作输出占空比50% ，频率可以调整的PWM波形

PWM模式1 其实就是PWM2 的取反状态，

### PWM的基本结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzQ2M2MwYjViM2YyMzAwMWYyMTk4ZGUxNzY3MTNhYmVfZFkzWHlBelFTaURXcHJZTHBLYURDVHpCN1E2QTdGRldfVG9rZW46R2tWdGJvMlNUb09Xd2p4ZWtaa2NjeTVLbnNmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

暂时无法在飞书文档外展示此内容

PWM 的参数计算

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjIyNzY4Y2JhZmE0MTBiMjM5N2E1MzE2N2FmZTZkNmRfZmMzSUtLNEZDS0dqWjVJRmdvazlSWldaU2RidExvV3dfVG9rZW46WG9id2JVZnBQb1I4RTN4NWhneGNLeW5PbkVmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

PWM的频率就等于计数器的溢出频率 Freq = CK_PSC(PSC+1)/(ARR+1) 频率等于时间除以周期（一段时间内出现了多少个周期，就是频率） 

PWM占空比计算： Duty = CCR （ARR+1） 可以看作为占空比计算=高电平/周期

PWM 占空比：从图上可以看出CCR 的数值应该是ARR+1 到 0 这个范围的 CCR等于ARR+1 的时候占空比就刚好是100%，如果将CCR 设置为102 那么占空比不会变化，所以CCR 的数值取决于ARR的数值，ARR越大那么CCR 就越大，对应的分辨率就越大。

 补充概念：MOS管（大功率电子开关）输出高电平导通，低电平断开，如果上下管都断开，那就是高阻态

###  舵机简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NGFhMmRjOWM0OWRjNGM0YTA3Y2Y0ZTQwNzNkNTcyNTBfWUhJWFN3bkpQTUF5OExjRmV2WTdYM3J0bjQxUDFxMzNfVG9rZW46Tmc0WGJsb1Zrb1RrUHN4Y3JCTmNsT2ZtbnJjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 舵机硬件电路

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MmViMmEyNGZkYmY0YWVhYmU2M2NlYmZjN2JlMjE4NzRfa05tdERWVEtJeHNEMEhVOHpESGdjZG1memVLZzdzWElfVG9rZW46UWhpYmJtb1Ztb1Vhb2t4Unp0N2NxdTNVbldmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 直流电机及驱动简单介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDU5OTAzNTQ1YmJiOTkxOTM0YjE2MjYxYzdmMTdkODJfem9ybERGVmIwTzJmWEVEcUpDbXI4R05kUlZqUTh5aGxfVG9rZW46VUozc2JLNEpib1owanF4ZFNRNGNDem5obkhlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### TB6612驱动模块硬件电路

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTgyNTZhMGI1ZTYwN2VhZmQ1YTZjZjJlZjViYTRjYjBfVGE4WGFrR3pUUEVMU0s1dXp1cW0zVHJFZjJwdk4wVTJfVG9rZW46U2FYYWJ0aTJnb2ZVWmt4T3dQcWNsZjRjbmdlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 呼吸灯 代码部分

初始化函数：配置主要分为三个部分 

暂时无法在飞书文档外展示此内容

结构体参数配置输出比较单元，四个函数对于四个单元

暂时无法在飞书文档外展示此内容

给输出比较结构体赋值（默认值）

暂时无法在飞书文档外展示此内容

配置强制输出模式

暂时无法在飞书文档外展示此内容

单独更改CCR数值的函数

暂时无法在飞书文档外展示此内容

重新映射（pin remapping）。

在电子电路设计和微控制器编程中，引脚重映射是指将特定功能的引脚重新分配到不同的物理引脚位置上。

这里我们可以用到这个引脚重映射函数

暂时无法在飞书文档外展示此内容

这里我们的 TIM2 是在 CH1 通道上的。如果该功能与 USART 产生冲突，就可以将引脚功能重新映射到别的引脚上，具体位置参考重定义功能列表。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmY3NzFhMTk0YTNlNDIzMGY1ZTYyNWUwMDEyZTU5NjdfeTFEYW9ORDJ3eEJHZW1iSGdHM0FRd0RkSXBZOXNJMEtfVG9rZW46SHVDS2JjTlk1b1R4Q3B4bmVBbGNKZURkbjZlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTE2ZDA2MmI2YjY3MTE2YzE0N2U4YTY5NjhhNjQ0OTNfeXdOQUFwRDJUU3dLWWpTOTRkM3p6bkZSSklXMVpXcldfVG9rZW46T3c1U2JwbWNCb1p4ZWt4Y1ZiaGNrblJWblNiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

这里的PA15端口，就有TIM2_CH1 这个通道，所以我们可以将PA1 引脚映射到PA15 上面，达到一样的效果

将TIM２　映射到PA15端口，并且解除端口的JTAD 复用

暂时无法在飞书文档外展示此内容

### 初始化函数部分

暂时无法在飞书文档外展示此内容

### 主函数部分，通过控制CCR的数值，达到呼吸灯的效果

暂时无法在飞书文档外展示此内容

### 程序效果：LED灯呈现高—>低—>高的亮度循环

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmI5Yzg5YTljNWFhZThhOWRlMjBiODY3OWMyZTdlZDNfUHZnVTNkV3NCQ1hHY1hoS2FYdWJUdTZhY0MzOEhaN3lfVG9rZW46Q3J3Y2JvN1dhb1UzTjV4WTZpTWNLMUo2bkZkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## SG90舵机代码部分

接线图

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDIwYmM5NWQxNDAzNmQ3MmE0ZmEyMmIwYjk1NzJlNTFfRzNNVlhOU3o1b0wxaldEb1VqTDNtUk5pZkNOYTZrWHlfVG9rZW46T1JqeGIxV0Z4b3hzaUZ4blExV2NPVE44bkhkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

注意，如果使用多个通道同时输出PWM，由于他们使用的是同一个时钟，所以频率必须相同，但是他们的CCR都是可以变化的

### 初始化函数

#### PWM部分

暂时无法在飞书文档外展示此内容

#### 舵机部分，通过公式换算，让角度数值更加直观

暂时无法在飞书文档外展示此内容

#### 主函数

暂时无法在飞书文档外展示此内容

#### 实现效果  舵机步距２０°，频率一秒

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OGJjYjUxOWI5MzA3YzkwZTIxNTFmMTI1MjIzNzhhOThfZFVFSGhqYzNleGpqd0pZUExIZXh3a2tqaVYxZU92ZllfVG9rZW46QnVBamJ1NU16bzRESlp4ekRSaWNzbWhybldmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## PWM TB6612驱动直流电机

### 硬件电路部分

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTFhOGExZGUyYzAwZDkzMDI5ZTZkZWMwZDc5YTM3MDNfQ2FmcmlJVkJkUWxDYk9CeDN2czY2WGJmdXZ5YmRybVBfVG9rZW46Q3IyU2JkWllHbzRST094SEJjZ2Nld2lmbjdjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 主函数

暂时无法在飞书文档外展示此内容

### 驱动部分

暂时无法在飞书文档外展示此内容

实现效果 直流电机速度变化，呈现在OLED屏幕上

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGQ5ODYzMmY2NjQ4YWEwN2EwMWVkZjlhMDRiMzBiNzZfa25OTEdLU251aDVkSUx6MVQyZlduZFB3ODkwNkRXMkZfVG9rZW46UmtUR2JvT0pZb0lybWl4emoyZmM3ejVNbkRmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 2.2输入捕获

### 输入捕获简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjMxZjczYWZlOGU1ODBiOGRkODM3ODdmZDYwYTNjYmFfb0V5SVd4R25LOU94ZE5RQ3lWajVMRVNOWGVYV0trU2FfVG9rZW46U0tQd2JnYTVWb1B0VnB4ZmR6M2NrSHN2bmllXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

一个通道内 IC 跟OC 不能同时运行

频率测量

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTBhYWUzYWI5Mzg3NjE2YTI0MTk4Mzc0Yjk1NGJjNmVfbjFVdHRDaVBWNEVLOEdZMGRYM2pqUUJBWDBZWHJwelJfVG9rZW46STVYaWJ5cUgxb1FyTzh4MlJhNWNMd25JbmRlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

测频法： 可以自定一个闸门时间T 通常是1秒 ，对上升沿进行计次，每一个上升沿其实就相当于一个周期，那么有多少个计次就是频率

测周法： 两个上升沿内，用标准频率进行计次，得到计次N　核心思路就是周期的倒数就是频率　公式推导

T周期　＝　N／标准频率　　而频率　＝　１／Ｔ　带入就得到了　频率　＝　１／（Ｎ／标注频率）＝标准频率／Ｎ　记１个数的时间　其实就是　１／标准频率　那么记Ｎ个数字就是N／标准频率

测量法跟测周法都是非常重要的方法，那么在实际使用过程中，应该如何选择呢？

　　首先，测频法适合测量高频信号，测周法适合测量低频信号，拿测频法来说，如果在闸门时间内，没有出现高电平信号或是只出现几个上升沿，但不能就此认定频率就是０，在计次N　很少的时候，误差就会很大　

　

　　而测周法需要低频信号，低频信号周期比较长，计次就会比较多，有助于减小误差，否则的话，比如标准频率为１ＭＨｚ　待测信号频率太高，频率为５００KHｚ在一个周期内就只能计一两个数，甚至一个都计不了，那我们也能认为信号无穷大吧

然后是测频法测量速度比较慢，因为是在闸门时间内进行计数，所以自带滤波，如果期间频率有变化，那么得到的其实是一段时间内的平均数值，相较而言，测周法只对一个周期进行计次，结果更新比较快，但是容易受到噪声的干扰

这里引入一个内容　如果高频信号用测频法　低频信号用测周法，那么高低的定义是什么，又该如何区分呢？

这就要靠中界频率的计算公式了

当待测信号大于中界频率的时候，选用测频法更合适，当待测信号小于中界频率的时候，用测周法更合适

### 输入捕获通道（详细）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2Y4ZWY4MTQxZDU2ZWJiZjg3MmI5Yjg2OTdkOThjZTFfR1ltcGlKVTRXNEpzVkdQSnR1cmhaODJDVkxRTXhyN0FfVG9rZW46TXlpTGJNS1Qyb3JHakR4b3ZwcmNOM2hlbktZXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

引脚进来，这里有一个异或门引脚，他的执行逻辑是当三个引脚有一个引脚产生反转的时候，输出引脚就产生一次电平翻转

暂时无法在飞书文档外展示此内容

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDNmMDgxOThkMDcwOGZkYjllOGY3MmQ5MjNkNWZjYmRfZ2VqYVVsdHp2SGNsM2JmWk5IclFuS242OHFSTEZhTkZfVG9rZW46RTBENWJiUmo3b0JpT2l4MjNPQWNYZDBEbmhoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

数字滤波器：以采样频率对信号进行连续采样，当采样个数连续都为高电平，数据才会有效

#### CNT 自动清0 硬件电路实现

这里可以看到TI1FP1 跟TI1F_ED都可以通向从模式控制器，从模式里面，就有可以完成CNT 自动清0 的电路

接下来我们就来看一下主从触发模式

##### 主从触发模式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjZiNjliOTQ3Yzk4YTYzYjAzMmZkYWQ5OTk3ZjIxM2RfS0Rjb0pzS0hCenhUYlQwVUw1dVpXTm9CQnNPbG5MU2hfVG9rZW46TEtVUWJDR3lOb29EZlF4ZUNrMGMwTVpZblpkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

主从触发模式就是 主模式 触发源选择 从模式 三个结构的简称

主模式： 它可以将定时器内部的信号，映射到TRGO引脚，用于触发别的外设

从模式：接收其他外设，或是自身外设的信号，用于控制自身定时器的运行，也就是被别的信号控制

触发源选择：可以看作从模式的一部分，选择指定的信号，得到TRGI，从而触发从模式，。从模式可以选择一项去进行执行，例如这里想要对CNT 进行清零，就可以用到Reset(复位)完成操作，实现硬件全自动

#### 输入捕获基本结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjljZGJhNjU5OGQ1OWNmMTIyMmZjYjUzZmFhZDIwZDZfT2thWWZZQlZWQnBLRXpFV2VQa0lsY0Q4MnVMVXhEUlZfVG9rZW46UjVPSGJBOTZ5b3djRGd4S1dNWGNueEZhbkhlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

暂时无法在飞书文档外展示此内容

#### PWMI 基本结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=M2I1OGIwNGU2Y2UwODYzNTgyYWFkMGZhZGJjNDM1YmFfSWx5ekh3aUNQcmZoV2pwMFhCOXhRdzJZTG9BdjdFaTZfVG9rZW46QldnQmJUTUMybzI3RU54TldKemMxS2lLbmJkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

这里上面的部分TI1FP1 配置为上升沿触发，触发捕获于清零CNT 正常地捕获周期，这时候，再来一路TI2FP2，配置为下降沿触发，通过交叉通道，去触发通道2的捕获单元，这时候会发生什么呢

看上图不难发现 最开始的时候 CCR1=CNT CNT清零 CNT 开始计数 当遇到下降沿触发CCR2 的捕获，所以这时候CCR2 的数值就是当前CNT 的数值，也就是高电平期间的计数数值，CCR2 捕获 ，并不会触发CNT清零，所以CNT 继续++直到下一次上升沿，继续下一轮 这时候 CCR1就是周期的计数，CCR2就是高电平的输出，有了这两个数值，就可以得出占空比了。

驱动函数配置过程

暂时无法在飞书文档外展示此内容

#### 初始化函数

暂时无法在飞书文档外展示此内容

#### 主函数部分

暂时无法在飞书文档外展示此内容

#### 实现效果 输入捕获测量PWM频率

输入捕获频率测量（我测我自己)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2NlNzU2ODdmNzgxNGFiNTYwNjllYzAxOTQ2YzQ5ZGRfVUtFdGZUd3VuMkFqNHhwdmhGUUxOU2syR3FmMFhuQXlfVG9rZW46SzB5TGJqVGlib1V2eEZ4dEJSR2MyTHFOblVoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 2.3TIM编码器接口

### 编码器接口简单介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmJkYzU3YTE1YmE1NjQyNWFiNjhkMjFiMjI3MTQzNjBfZmdZZ0gwS1pseWhsSUd1YVJHV2hJOXM0Rlp6N3dDbDdfVG9rZW46WXl2Z2JYMFFpb3A5QUV4QUtTcmNWSGdXbndnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

方波的频率其实就代表了速度

### 编码器接口测速原理

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmU0NTVkZTVhYjE5ZDQ3NDc5YjlmMmZjYTM0MWRhZmNfV090ZWNtdmtLTldCWnl4ME41UHF4UXA0MEdMYWg3Q3hfVG9rZW46VUd4ZGJrWlcyb290ekt4WTZxdWNPZG1QbmVrXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

TIM编码器测速本质上就是测频法，在指定时间内，对高电平信号进行计次

编码器接口的设计逻辑就是，首先把A相和B 项的所有边沿作为计数器的计数时钟，出现边沿信号的时候，就自增或者自减，如何判断自增还是自减？当出现边沿信号的时候，我们去判断另一项的状态，如果这时候另一项为低电平，那么就为正转，如果为高电平，那么就为翻转，以此判断正交编码器的旋转方向。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OWU0YzliNWY1NGQzY2E3YzI4NmYzZTEzYTBlMGU3OTBfZHVaOVpTamRYU0RmVEFWclY4SUhjUmowZ0Y3aTJrRVFfVG9rZW46TkpnSWI0SjBpbzhGRWx4SUNiZGNROEFlbkZmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

这里的从模式自动电路也是一样的，当出现了边沿信号，并且另一向为低电平就控制CNt自增 否则控制CNT自减

### 编码器接口基本结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWU3ODk5YjEwMTYxMTU0NTcwNjA2MWU0ZjEzYTNjYTBfZWJqWk9WbGRhQjd5TnZzV0wwRVRhWDdvMDJ3M3NsaHhfVG9rZW46RGFhTGJwRk01b2tnaU54UW0wM2NUY0dsbkZlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 工作模式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzVlMmM0ZDQzNTRkNGU0ODc0YWVmZDBlNjJhYjZjZjVfNnVZRDh4RDNmOHBIQXZPTjlLUkNkNllUY2t6ajhobFBfVG9rZW46UGlaRWJYTzRqb3dwaWN4ejRzamNZT2VGbkRjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

因为旋转器编码接口有两个向的输入，可以选择只对一个向进行计数，一般情况下，我们都对两个向进行计数

正交编码器抗噪声原理

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjFjZWEyNWRiMGU3ZDljZDhhMjBjMmEyOWFiMWY5ZTNfS1Fpc2M4Y3FFbDd4OTc4YmJBMFBGcU5NZjhMS09VOUZfVG9rZW46RE1LbWJRZGQ1b0F6OGt4WkhCMWNFc2FMbm1jXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

当一个向的电平不变化，另一个向的电平连续变化的时候，这时候，由于一项保持高电平或是低电平，对应表的关闭，根据跳变信号向CNT计数器就会反复的自增自减自增自减，那么最终的数，还是毛刺信号前的数值，不会收到干扰影响。

总结：编码器接口模式基本上相当于使用了一个带有方向选择的外部时钟

### 代码部分

初始化流程

暂时无法在飞书文档外展示此内容

GPIO 模式选择原则：一般可以看外部模块输出默认电平，如果外部模块空闲默认输出高电平，我们就选择上拉输入，默认输入高电平，反之，如果外部模块默认输出低电平，我们就配置下拉输入，默认输入低电平，和外部模块保持默认一致，防止默认电平打架，这是上拉下拉的选择原则，不过一般来说，默认高电平，这是一个习惯的状态，所以一般上拉输入用的比较多，如果你不确认外部输入的默认状态，或是外部信号输出功率非常小，这时候就尽量选择浮空输入，因为他没有上拉或是下拉电阻干扰外部信号，缺点就是当引脚悬空的时候，容易受到干扰

#### 主函数部分

暂时无法在飞书文档外展示此内容

初始化函数部分

暂时无法在飞书文档外展示此内容

#### 程序现象

OLED 屏幕呈现编码器正/反旋转速度 频率1 秒

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=M2RlYjUyOTliMmZhOGI5MGMxNDcxZmNlMjA3ZWZlMjBfZEZHTlJIMFVweWFBMW9JYUJCWmJwYzhUNEdYYWhWNEpfVG9rZW46UVlEcGJod3R2bzlEMXd4V1lpMWNSQk9lbkNkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# 3.ADC 模拟-数字转换器

### ADC简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmY3MGZlNDkyOGZhOTUwM2I2YmJlZTU2MDkyMGYxZWZfYWdhNlFTRTNYRGdOVVNBNGs4YU9Rd05ISWRjR2JGa0dfVG9rZW46SVk0eGJ0TFg4b2VIZkl4MzZkYWNkTW9mbldiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 逐次逼近型ADC ADC0809

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmQyNWE3YzA3NWU4ZDEwOGFjNGQ0NTM4NzdlODI5YzZfUDBMaWVtNFVES0p6bDdqckU1OGlhTFRLY2QwZHk5OE1fVG9rZW46RUk5cWJLMWhtb1hVUTd4N2lRR2NaeE1GbmZ0XzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

暂时无法在飞书文档外展示此内容

注：一般参考电压的正极跟ｖｃｃ相接　参考电压的负极跟ｖｃｃ接在一起，所以对于ADC０８０９来说输入电压决定了ADC的测量范围

### stm32 ADC框图

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MWQ0ODViMzdiODBhZDNiZDg1ZTE5Y2UxNzBiYTJjYWRfOWpibjRxaWxqTkQ5Ukd6MFFKeTNjbDdyTjNqZ1dqcjhfVG9rZW46VGNXbmJEUE5kb0dPYjB4cTYzZmNOWlpmbjZnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

暂时无法在飞书文档外展示此内容

#### 规则通道

在 ADC 转换中，规则通道如同餐厅菜单，有多个可供选择的通道对应不同输入信号。寄存器恰似盘子，一次只能存一个通道的转换结果。而 DMA 就像上菜小助手，在 ADC 转换后自动将结果从寄存器转至内存，防止数据覆盖，提高数据传输效率，减轻 CPU 负担。

#### 注入通道 

对于 ADC 转换，注入通道类似 VIP 通道，能一次上四个 “菜”（处理多个数据）且无需担心数据覆盖。不过通常情况下使用规则通道即可，再配合 DMA 这个 “上菜小助手”，能高效地完成数据转换和传输任务。

对于 STM32 的模数转换器（ADC）而言，其触发 ADC 转换的方式主要有两种。其一为软件触发，即通过在程序中手动调用特定代码指令来启动转换过程。其二是硬件触发源，其中包括注入通道触发源和规则通道触发源。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTQ3YjkwNmMyNDlhYjE2NTNmYWFhNmM4NzFhOTIxYmNfbXpmTlA0eU9UaWNvVHExd3poQ0ZRcGxWdnM0QjhSdFVfVG9rZW46QzhFVGJSbkxLb0VWREd4QzB6dmNKYnlkbk9jXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 这是一种利用定时器触发 ADC 采样的方法，其原理如下：

**一、定时器部分（TIM3）**

1. 定时器设置为 1ms 定时：
   1. 通过配置 TIM3 的相关寄存器，使其产生周期为 1ms 的定时信号。这意味着每隔 1ms，定时器会触发一个特定的事件。
2. 更新事件选择为 TRGO（触发输出）：
   1. 当定时器达到设定的时间（1ms）时，会产生一个更新事件。将这个更新事件配置为触发输出（TRGO）模式，意味着定时器会在更新事件发生时，向外部输出一个特定的触发信号。

**二、ADC 部分**

1. 选择开始触发信号为 TIM3 的 TRGO：
   1. 通过配置 ADC 的相关寄存器，将其开始触发信号源设置为 TIM3 的 TRGO。这意味着当 TIM3 的 TRGO 触发信号到来时，ADC 会开始进行一次采样转换。

**总体工作流程**

1. 定时器 TIM3 按照设定的 1ms 周期进行计时。
2. 当 1ms 时间到达时，TIM3 产生更新事件，并通过 TRGO 输出一个触发信号。
3. ADC 检测到 TIM3 的 TRGO 触发信号后，开始进行一次采样转换。
4. 如此循环往复，实现以固定的 1ms 频率对输入信号进行 ADC 采样。

这种方法的优点是可以避免使用传统定时器中断方式进行 ADC 采样时频繁进入中断带来的高资源占用问题。通过硬件触发的方式，使得 ADC 采样更加高效和可靠，同时减少了对 CPU 的中断请求，降低了系统的负担。

#### ADC模拟看门狗

STM32 的 ADC 模拟看门狗用于监测特定模拟输入通道。可设置高、低阈值，当输入值超出范围会触发中断，适用于电源监测、传感器监测和故障检测等场景。配置时需使能 ADC 和模拟看门狗功能、设置阈值、选择监测通道并配置中断。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MzQ0OTc4ZTQyYjk0NTk5MmQyODJlY2M3NzBhMzRhNjRfOE5SR21La3lWeGxXRUxUOHBvRU1CS2c5SGVQNUdBQnBfVG9rZW46TklmS2JTaW5Gb2JqTFR4YktJTWM2eVhrbmhmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

ADC基本结构(总结）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTZiZjEyMjI1ODk2MWNhZmI2NDc4MmIyYWMyZjZjOGJfR3FSYmhucmlsRFVXZHBhUVh3aDEwekJGWnkzZDhxU3FfVG9rZW46TE1Wc2JvcEhjb09sd0x4MXFBaWNGcjB1bnhiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

暂时无法在飞书文档外展示此内容

#### 输入通道

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzIxYzg1MTYwYzZlZDNiMGRiYTE5ZDE3NGRiMmRjZTRfclFKblZQbHZWZHcwRjRjbUR1eTZ3WlRiak9VSFJLZzBfVG9rZW46S3RLdmIxbnNJb1NPUEd4b0RjY2NyNGNqbmZXXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### STM32 的 ADC 有四种转换模式：

1. 单次转换模式：启动一次只进行一次 A/D 转换。
2. 连续转换模式：一旦启动，将连续进行 A/D 转换。
3. 扫描模式：可按顺序对多个通道进行转换。
4. 间断模式：可以对选定的一组通道进行分批次转换。

#### 触发控制

在 STM32 中，ADC（模数转换器）可以通过多种方式触发转换

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTAwZDc2YjgxYzA1NjYxZDY2YmFjOGZhNTRlZWRlMDBfSE8xclZsckN1WFFydUlua04xWHMyWVB6WEdkTGlNM3pfVG9rZW46RlJQc2J3UjJLb2F3RmN4a0l0dWMwQ0llbmJnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 数据对齐

**一、ADC 数据位数与寄存器宽度** 12 位 ADC 理论可输出 4096 个量化电平值，结果在 0 到 4095 变化。数据寄存器 16 位宽引发数据对齐问题，需确定 12 位数据在 16 位寄存器中的放置方式。

**二、数据右对齐** 右对齐时，12 位 ADC 转换结果放于 16 位寄存器低 12 位，高 4 位为填充位。多数情况合理，能准确反映转换值，便于后续数据处理，可直接读低 12 位。

**三、左对齐应用场景与局限** 左对齐下，12 位结果在高 12 位，低 4 位填充。用于低精度场景，如只需前 8 位数据时，但会降低分辨率。左移数据使数值变大，左对齐操作可能导致数据不准确解释，尤其需高精度结果时。综上，一般选右对齐保证准确性，左对齐适用于特定低精度场景。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzAzOTFlMTZmNTY1NjljYjVjZmM4NjJkYmM1NzQ0YzlfS1FpOHRZamNuNVQ1RVBZeEQ2SHg3VFZUenl0eUtlQUJfVG9rZW46TWs4cWI1d1Z1bzVOOWd4ZTBYbWNaMW5MbnJjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 转换时间

**一、AD 转换耗时类比及步骤概述** ADC 转换如同厨子做菜需时间。其步骤有四步：采样、保持、量化、编码，可分为采样保持和量化编码两大步。

**二、量化编码** 量化编码是 ADC 逐次比较过程，位数越多耗时越长。

**三、采样保持电路** 若量化编码时电压变化则无法定位输入电压。故先设采样开关，开开关用小采样电容存储电压，存储完关开关再进行 AD 转换，确保量化编码期间电压不变以定位未知电压。采样保持过程中，闭合开关一段时间后断开产生采样时间。

**四、总转换时间** ADC 总转换时间为采样时间加 12.5 个 ADC 周期。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTA5ODg2NzViZTBmODZiMDNhNWJjYTg1ZjdkOGRjMjlfc2xxSXNmWVZBTkRUNURzT1BqNkpwNUsyUnVHdkdmb0JfVG9rZW46TzVSWGJTUXg2b2I2R2Z4RE4zUGNUeHNlbmZjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 校准

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDJkM2IwZDFkZDM4NTcyMzAyZWYyYzEyMDY3NDNkNjFfWGVMRkFmT2xmMmthTGNKdjBYS0ZacWFpNXpxZlNtZkNfVG9rZW46U2lTN2I4ZElybzQ4YXd4VGFnYmNpcUFBblFjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## adc转化单通道

#### 硬件部分

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjY3NjY0NjI3MWFlYTBjNjYyZTBmMWQ5ZjQyYTU2NmNfS2gyUk1GcDU1TW5VTEFxOTR0S01Dckx2UHJYelFvcURfVG9rZW46RzdDTWJPNGJCb3FKTnh4SWh4NmNJODJlbm9lXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 代码部分

配置过程

暂时无法在飞书文档外展示此内容

#### 初始化文件

#### 主函数

#### 程序现象

### DMA简介

**一、DMA 外设权限**

- DMA 外设可直接访问 STM32 内部存储器，包括运行内存 SRAM、程序存储器 FLASH 和寄存器等。

**二、DMA 功能**

- DMA 可提供外设和存储器或存储器和存储器之间的高速数据传输，无需 CPU 干预，节省 CPU 资源。外设指外设的寄存器，如 ADC、串口的数据寄存器等；存储器指运行内存 SRAM 和程序存储器 FLASH，用于存储变量数组和程序代码。

**三、DMA 通道特点**

- DMA 有 12 个独立可配置的通道，进行数据转运时占用一个通道，多个通道可互不干扰。每个通道都支持软件触发和特定硬件触发。若为存储器到存储器的数据转运，只能使用软件触发；外设到存储器的转运不能用软件触发，需硬件触发，如转运 ADC 数据需等 ADC 每个通道 AD 转换完成后硬件触发 DMA。存储器到存储器一般用软件触发，外设到存储器一般用硬件触发。且每个 DMA 通道硬件触发源不一样，使用某个外设的硬件触发源需用其连接的通道，不能用任意通道。

#### 存储器映像

**一、存储器映像概述**

- 了解 STM32 中的存储器及地址安排即存储器映像内容。计算机系统核心关键部分是 CPU 和存储器，存储器内容地址分 ROM 和 RAM 两种类型。

**二、ROM 类型**

- ROM 是只读存储器，非易失性，掉电不丢失。分成三块，一种是程序存储器 FLASH（主闪存），用于存储 C 语言编译后的程序代码，是下载程序位置，一般运行程序也从主闪存开始。选项字节存 FLASH 的读写保护及看门狗配置。

**三、RAM 类型**

- RAM 是随机存储器，易失性，掉电丢失。RAM 区域分成三块，一是运行内存 SRAM，用于存储变量、数组、结构体地址，相当于计算机中的内存条。二是外设寄存器，存储各个外设的配置参数，其存储介质也是 SRAM，但习惯上运行内存叫 SRAM，外设寄存器直接叫寄存器。三是内核外设寄存器，存储内核各个外设的配置参数，内核外设如 NVIC 和 SysTick，因内核外设与外设寄存器不是同一厂家制作，地址被分开。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDE0MGNkZGEzOWQ0NWY1YjdiYjg0ZGU3MmU3NzBlNDFfUDJTc1dYbVZEaEU0M05oQXFBTXFyMXhVdmgxMldhaFFfVG9rZW46UXM3NGJ1VzN2bzFLd1p4bmZZUmNOUDMxbmtmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

**一、STM32 存储器地址范围**

- 在 STM32 中，所有存储器被安排在 0 - 8 个 F 这个地址范围内。
- CPU 是 32 位的，寻址范围大，最大可支持 4GB 存储器，而 STM32 的存储器是 KB 级别，地址使用率不到 1%。

**二、Reserved 区域和地址 0 的别名区**

- 图中有灰色填充的是 Reserved 区域，即保留区域未被使用。
- 地址 0 没有存储器，别名是到 FLASH 或者系统存储器，取决于 BOOT 引脚。
- 程序从 0 地址开始运行，可映射到 flash 区域从 FLASH 执行，映射到系统存储器区从系统存储器运行 BOOTloader，映射到 SRAM 从 SRAM 启动，由 BOOT0 和 BOOT1 两个引脚决定。

**三、FLASH 区用途**

- 从 0800 开始的 FLASH 区用于存储程序代码。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTE0MDA4YWEyMTljOWVlZDU0Nzk1YmNhYWE3ZjA5YmNfb005NmZVQ2FzR2ZtTVlBVlBvd2V4NVBKV3Ywd3BKVDhfVG9rZW46RXZscmJTM0J5b3E5czZ4VDBmSGNiREY1bm5lXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### DAM框图

**一、整体结构**

- 左上角是 Cortex-M3 内核，包含 CPU 和内核外设等，其余部分可看作存储器。外设可视为寄存器，也是一种特殊的 SRAM 存储器，是连接软件和硬件的桥梁。
- 为高效访问存储器设计了总线矩阵，左端是主动单元，拥有存储器访问权，如内核的 Dcode 和系统总线，Dcode 总线专门访问 FLASH，系统总线访问其他东西。DMA 也有主动权，DMA1 有 7 个通道，DMA2 有 5 个通道，可分别设置转运数据的源地址和目的地址独立工作。

**二、仲裁器作用**

- 下面有仲裁器，因为多个通道只能分时复用一条 DMA 总线，产生冲突时根据通道优先级决定先后。总线矩阵处也有仲裁器，若 DMA 与 CPU 同时访问同一目标，DMA 会暂停 CPU 访问防止冲突，但仍保证 CPU 得到一半带宽以正常运行。

**三、DMA 结构组成**

- AHB 从设备是 DMA 自身的寄存器，连在右边 AHB 总线上，使 DMA 既是总线矩阵主动单元可读取各种存储器，又是 AHB 总线上被动单元可被 CPU 配置。
- DMA 请求是触发信号，右边触发源是各个外设，是 DMA 硬件触发源，如 ADC 转换完成、串口接收数据时向 DMA 发出硬件触发信号，之后 DMA 执行数据转运工作。DMA 结构包括通向各个寄存器的 DMA 总线、多个可独立转运数据的通道、仲裁器用于调度通道防冲突、AHB 从设备用于配置 DMA 参数以及 DMA 请求用于硬件触发数据转运。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTNkMzk5ZDVkYjQ1NzA3MGQ2YzI1ZGNkNTE2MGQ2NzZfZnRmdmtDU0ZXMzVpb3dHNXhBN0pOQzl5QVNTQkl4WEpfVG9rZW46VWFpSGJCMkpkb05lcnZ4WTJPV2NVSmhKbkFoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

**基本结构**：

- DMA 转运可从寄存器到存储器，也可从存储器到存储器，由方向参数改变转运方向。寄存器和存储器都有三个参数：
  - 起始地址决定数据从哪里来、到哪里去。
  - 数据宽度可选择字节（Byte，`uint_8`）、半字（HalfWord，`uint_16`）和字（Word，`uint_32`），就像马路决定一次转运的数据宽度。
  - 地址是否自增参数，指定一次转运完成后地址是否自增，外设一般不自增，存储器需要自增以避免数据覆盖。
- 传输计数器用于指定数据个数，是自减计数器，结束后地址自动回到起始地址方便下一轮转换。自动重装器决定转运模式，不重装为正常单次模式，重装则自减到 0 后回到初始数值开始下一轮，如转运数组一般用单次模式，ADC 扫描模式加连续转换时，为配合 ADC，DMA 要变成循环模式。
- 触发源选择可决定如何进行 DMA 转运，具体参数由 M2M（Memory to Memory）选择。软件触发一般用于存储器到存储器的转运，以实现最快速度的触发与转运。注意，写入传输计数器数值时，必须关闭 DMA_cmd。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzZlNzM3OGVkNzcyODA3MGMxNjQxMjAxOTJjMTdjMWFfekNWNm5jTGpVcEVFY0NKU0NUbVRxYXdvTENlMGNCd1RfVG9rZW46QmM0d2J1cU9lbzhxM0R4VVV2dWNhZlRhbkpaXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### DMA 请求

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTE3OWIxODMxZTEyMjYwMjZmMmRkY2RlZGJmZTdkMmJfb1lWUkdudENicUdneFlBOVpmSFZBWkxHWVlKOXhqWE9fVG9rZW46QTljaWJYSFh4b3prTEZ4UFp6MmN6QW55bnFlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

数据宽度

如果源端宽度跟目标宽度不一致，那么就会将数据高位补0，低位写入，总的来说就是低位补高位补零，高位补低位舍高位

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjQ4NTNlZmRkZGMzYmU0ZGExZmE4YWJhZjMwNGUyMzlfSUpLaDVUSlVIQkkxa0VoZ1BLN2pweVhCZzN5d2ZnZlJfVG9rZW46TGFwWGJzOXBjb0dHb0R4bTRrVWNKTXFObnBnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 硬件部分

#### 初始化函数

#### 主函数

#### 程序现象

# 4.USART串口协议

### 通讯接口

**一、双工模式**

1. 全双工：通讯双方都能够同时进行双向通讯，一般需要两条数据传输线，比如串口通讯（一根 TX 发送，一根 RX 接收）、SPI（一根 MOSI 发送，一根 MISO 接收），发送线路和接收线路互不影响。
2. 半双工：通讯双方需要异步通讯。
3. 单工：只有一方可以接收，另一方为发送。

**二、时钟**

1. 如果发送方发送数据，接收方需要通过时钟线知道数据是怎样的。像 IIC 和 SPI 有单独的时钟线，是同步的，接收方可以在时钟信号指引下进行采样。
2. USART、CAN、USB 没有时钟线，需要双方约定一个采样频率，并且加一些帧头帧尾等进行采样数据的对齐。

**三、电平特性**

1. USART、IIC、SPI 都是单端信号，引脚高低电平是对 GND 的电压差，通讯双方必须共地（把 GND 接在一起），所以这三个通讯引脚还应加上一个 GND。
2. CAN 和 USB 是差分信号，通过两个差分引脚的电压差进行数据传输，通讯时可以不需要 GND，但 USB 协议里有一些也需要单端信号，所以 USB 还是需要共地。差分信号抗干扰能力强，传输距离远。

**四、设备**

1. USART 和 USB 属于 1 对 1 点对点的通讯方式。
2. IIC、SPI 以及 CAN 是多设备的，可以在总线上挂载多个设备，主机可以指定与哪个设备进行通讯。点对点通讯就像老师找你去办公室谈话，只有两个人，直接传输数据即可；多设备通讯就像老师在教室里上课，面对多人，需要有一个寻址的过程以确定通讯的对象。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmRhNGEwY2M1NDU3NTAzNDJkZWY0ZWQ1ZWQ1MjBlMWNfQXVib0tmQkN1VXQ4Slpta21ibXlZaXNjZk01aktlTWZfVG9rZW46VEJQS2I4UjBib3VwZ3l4UTZIR2NBTzJIbm5jXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 串口通讯

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjNlZjA3YzdlOTE1YWI2ZDE2NWE3NjVmZjkwOTRiYjFfODl4bHZ3bjM0aVRDdFk4ZlZROEx2cjdSbU5EMUd5Q25fVG9rZW46RVl0RGJvYUdIb0w0ZER4NmxOSmNtMkdObkhkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 硬件电路

1. TX、RX 的高低信号都是相对于 GND，属于单端信号，所以 TX、RX、GND 这三个端口通常必须要接上去。如果两个设备都有独立供电，VCC 可以不接。
2. RX 跟 TX 是交叉连接的，因为一个设备的发送要另一个设备接收，另一个设备的发送要一个设备接收。当只需单向数据传输的时候，可以只接一根通讯线，退化成单工通讯。
3. 当电平标准不一致的时候，需要加电平转换芯片。像这种直接从控制器里面出来的电平，一般都是 TTL 电平。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDEyMDMyYzMzMGE3ZmI5N2YyNzEwYmYzNWFkOGM2ZDdfYmtCekVVTFpXcUJ4RVlhQm5KOHl3bzJkMmdlMGdXWkFfVG9rZW46WExzVmJXMVp5b0xUZER4MjVQSGM1RWF0bmZnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 电平标准

**一、电平标准的概念** 电平标准是数据 1 和数据 0 的表达方式，即传输线缆中人为规定的电压与数据的对应关系。

**二、常见的单片机电路电平标准 ——TTL** 在单片机电路中最常见的是 TTL 电路，5V 或者 3.3V 表示逻辑 1，0V 表示逻辑 0。

**三、串口通信中的其他电平标准**

1. **RS232**：电压范围较大，通常采用负逻辑，即 -3V 到 -15V 表示逻辑 1，+3V 到 +15V 表示逻辑 0。
2. **RS485**：采用差分信号传输，抗干扰能力强。通常以两线之间的电压差来表示逻辑状态，具体电压值会根据不同设备和应用有所差异。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzBhODFiMjRlOTFlYWEwYzRhOWNjZjFjZjM1ZWYyMjNfRGhGZ2kzc0xxT3ExdXRmampSbUo2NjZLUkdlTmkzY0tfVG9rZW46RFNWemJLeGpzb2U5WTl4SDNjd2NLOHZrbkJlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 串口参数以及时序

**一、串口数据格式**

串口发送数据时，会将每一个字节包装在一个数据帧中。这个数据帧就像是一个小包裹，里面装着要传输的数据。数据帧主要由起始位、数据位和停止位组成。

通常情况下，数据位是 8 位，这意味着一个数据帧可以传输 8 个二进制数字。不过，如果加上一个校验位，那么数据位就变成了 9 位。校验位的作用是帮助检测数据在传输过程中是否出现错误。有效数据位还是8位

**二、串口通讯参数**

1. **波特率**：串口采用异步通信方式。波特率就像是数据传输的速度。比如，波特率为 9600 表示每秒可以传输 9600 个二进制位。不同的设备可能需要不同的波特率来确保数据能够正确地传输。
2. **起始位**：它是数据帧的开始标志，就像一封信的开头。起始位通常是一个逻辑 0 的位，它告诉接收方数据即将到来。
3. **数据位**：这是实际要传输的数据内容。可以根据具体需求设置数据位的位数，常见的有 8 位。数据位中的每一位都代表一个二进制数字，可以是 0 或 1。
4. **校验位**：校验位用于检查数据在传输过程中是否出现错误。有奇校验、偶校验和无校验等不同的校验方式。例如，在奇校验中，数据位和校验位中 1 的总数为奇数；在偶校验中，1 的总数为偶数。但是如果两个数据 同时出错，这种校验方式就不合适了，如果想要更高的检出率，可以了解一下CRC校验
5. **停止位**：停止位标志着数据帧的结束，就像一封信的结尾。停止位通常是一个或多个逻辑 1 的位，它告诉接收方这个数据帧已经传输完毕。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTk2ZGI3NDY1Mzc0MDJiNzBlNmMzZjdkZTIyNTdjZGRfOERZcVpRWTNNaUNOUGRJeXNrMWZxZUp5UkcxTm55cEZfVG9rZW46UkRSaWJrOFVCb203RzV4VWRzMWMyVERxbmtlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 串口时序

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjQ3OTI3YmM1NDA1MjY3OWQ0N2VmYjAwMGU4YzczNDdfRldBVUJQOXBTQXdFTENOS09uWVNUWlUwSGl0Q01lZE9fVG9rZW46WlQzQWJ0R1hPb2xnMm94eWI0VWMzZlljbkJiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### STM32 USART外设

USART 是 STM32 内部集成的硬件外设，具有以下特点：

- 能自动生成和接收数据时序，将数据从 TX 引脚发送、在 RX 引脚接收后存于数据寄存器。
- 自带波特率发生器，最高达 4.5 Mbits/s。
- 可配置数据位长度为 8 或 9，停止位长度有 0.5、1、1.5、2 可选，校验位有无校验、奇校验、偶校验。
- 支持同步模式、硬件流控制、DMA、智能卡、IrDA、LIN。
- STM32F103C8T6 的 USART 资源包括 USART1、USART2、USART3。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzliMzdjOGNhYzcwZWI2YTZkMDJkNzEwZGQzZTI0NThfYUhYSGxxcDVrV08xM2RzYk9XVml2eEFRQXFPZVY4TUNfVG9rZW46WnhNVWJDekx6b0NTM0x4ZE5ZcmNNVk9BbkRlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### USART框图

1. 在 STM32 中，发送数据寄存器（TDR）和接收数据寄存器（RDR）在程序上表现为数据寄存器 DR，但实际硬件分为两个。
   1. TDR 只写，用于存储待发送数据。
   2. RDR 只读，用于存储接收到的数据。
2. 发送 / 接收移位寄存器：
   1. 发送移位寄存器将数据逐位从 TDR 取出发送。
   2. 接收移位寄存器将接收的逐位数据拼接存入 RDR。
3. 数据发送时，TDR 检测发送移位寄存器是否在执行移位操作。若未执行，将数据全部移动到发送移位寄存器准备发送，同时置标志位 TXE（发送寄存器空）。当 TXE 置 1 时可在 TDR 写入下一个数据，但此时数据其实还未发送出去。发送移位寄存器在发生器控制驱动下向右移位，将数据一位一位输出到 TX 引脚，与串口协议规定的低位先行一致。数据发送后，新数据会自动从 TDR 转运到发送移位寄存器，若未完成 TDR 会等待，一旦完成 TDR 立即转移过来。TDR 与数据寄存器的双重缓存可保证连续发送数据时无间隔，提高工作效率。接收数据寄存器也是同理
4. 硬件数据流控，串口的硬件流控制主要是通过 RTS/CTS（请求发送 / 清除发送）和 DTR/DSR（数据终端准备好 / 数据设置准备好）等信号来实现。当发送方准备发送数据时，会查看接收方的 CTS 信号，若 CTS 有效则发送数据，否则暂停发送。接收方可以根据自身缓冲区状态控制 CTS 信号。这样可以有效避免数据丢失和缓冲区溢出，保证串口数据传输的稳定和高效。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWZiNjBkOTJiMjE5MmJmMjQ3ZWVjNDA3NDVjOTY0NjZfOVV5OHA3MWV5dHpNd2FtWWd1akV2UXZ2WHJ2cmRER2lfVG9rZW46U0JVWGJOQm02bzZOY2V4VEtOUWM2dDZYbnlnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### USART简化结构图

- 波特率发生器的时钟来源是 PCLK2/1，本质上是一个分频器，用于确定串口通信的速率。
- 发送控制器和接收控制器分别控制发送部分和接收部分的寄存器。
- 通过 GPIO 的串口复用，连接到 TX 引脚和 RX 引脚。
- 在软件层面，只有一个 DR 寄存器，进行数据发送时走发送路径，进行接收时走接收路径。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OWU5NTllNmVhNTgzZGI5MjY1YmM2ODU0YmQ3MmQ5OGVfcElVajVIWm8yS1I0TFlHaFpEUTZjQnlJSmJhNlpocDVfVG9rZW46RHBHSWJoMHRwb0RKZWR4QlhWamNBSVZXbk5lXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 数据帧

1. STM32 串口通信中，数据帧字长可设置为 8 位或 9 位。
2. 8 位字长的数据帧通常由起始位、8 位数据位、校验位（可选）和停止位组成。
3. 9 位字长的数据帧会增加一位额外的数据位，可用于特定通信需求，如多处理器通信中的地址标识位。

式，

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjI3NjdlNGIzNTI5MjY4NzZmODcwYzA3NWFlMGUxOTRfelU1eUM1dkpLQ0dVWDVySEtrTnc4QVg1VU9FRmNGeHpfVG9rZW46TGhuaGI0SlhHb25vR1B4bDkwNWNreHFpblloXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 起始位侦测

1. STM32 串口发送只需定时反转高低电平。
2. 串口接收需保证每次采样在电平中心以防止数据错误。
3. STM32 接收电路在起始位进行 16 次采样，检测到低电平（0）时判断有数据来。
4. 实际电路中有噪声，需连续 3 位中有 2 位为 0 才判断为 0。
5. 检测到噪声后在状态寄存器置 NE 标志位提醒数据有噪声。
6. 第 8、9、10 次采样在数据中间，接收数据位时在这三次进行采样以保证在中间位置，这是起始位侦测和采样位置对齐策略。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Mzc5ZjRmMTcwYWQwYTVjYzA5MjhiYzI3M2Y3MGJjZGFfRURIMWllYkJONnlWUmVsTnFiUXZYWXNhQnFsQzNKaXlfVG9rZW46SXRRWWJGVHZzb0x0WHl4Z2xUaWNSRkZBbkNkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 数据采样

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDUwZGJhZjNlNDNhYmYxYmM1OWFkZjI0MzUxNWU2ZmJfMlN2QW9tOVplZHFrSHpLVUk5TWtPZ3lGaXdaRXZWZXRfVG9rZW46RkZwb2J1Mjgzb0I4NzJ4SVh5dWNOQTB0bkFoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 波特率发生器

发送器和接收器的波特率由波特率寄存器BRR里面的DIV确定

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTYwNDg2MWZkYzhkZGIyZGE1ZWY1MDE3ZTdmODRmM2ZfMHNuS1NsbXRaR3VPT1NHeWlZWnRtbndBV3Z4alBrcDRfVG9rZW46UG1EcGJlNmp4b053NXJ4UVNzYmNsUUFubnRkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 串口发送&接收

###### 硬件电路

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDIzY2RhMzFmZGY3NzkyZGY0ODNmYjQ1YjhhN2E5M2NfUHlZdGtZWHE2UEVTYzFCaE11V0dCU1kxdkpURklvTHpfVG9rZW46RzlqRmJXOWJ5bzY2OFN4WFRXeWNsVWRGbnZoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 发送 主函数

暂时无法在飞书文档外展示此内容

###### 初始化部分

暂时无法在飞书文档外展示此内容

##### HEX数据包

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTU1ZmI3OTc1NDdhZGUxMDViMmM2ZjVmOGQ3NzI1NWZfRTc4V1RpTm9MS211ZWVqdjdkYklEd2twYndaajBjcTJfVG9rZW46RzhvMGI2bFFDb3VsSnB4SE8zbmN4bnZKbkFlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

###### HEX数据包接收—状态机、

暂时无法在飞书文档外展示此内容

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YWEwNzIyODgyZjY2ZGYyMmM0YjZmNTQzMGViOTA3MmJfTFYzb3RaUjdmOUFGNlhoZWxXRjVFWkN3amR5NlljcGpfVG9rZW46T1dKMWJPdHhFb0FPbW94MFRzdmN0NzJmbmhoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# IIC通信

### IIC简介

主要的两根通讯线，一根SCL串行时钟线，SDA串行数据线，作为一个通讯协议，它必须要在硬件和软件上，都做出规定，硬件上的规定，就是你的电路应该如何连接，端口的输入输出模式都是啥样的的，软件上的规定，就是你的时序是如何定义的，字节如何传输，高位先行还是低位先行，一个完整的时序，由哪些完整的部分构成，硬件的规定和软件的规定配合起来，就是通讯协议，这也能够更好的帮助我们学习IIC

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTkyMzU2Y2JjZjdiOTI1ZGFkNmJhYWQzNGE4YjA5ZWZfUTlTRzdiMFpzZWh4bGdsZzdkcEIxUXNWNXVQdFBRWEJfVG9rZW46TGJFU2JTTnQ1bzZHcVF4ZXVia2NjZHZZbnFkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 硬件规定

可以看到，最右边的CPU就是我们的主机，他的权限最大，在空闲状态下，主机可以主动发起对SDA的控制，只有在从机发送数据和从机应答的时候，主机才会转角SDA控制权给从机，这就是主机的权利，下面的就是IC从机，从机的权利比较小，对于SCL时钟线，在任何时刻都只能被动的读取，从机不允许控制SCL时钟线，对于SDA数据线，从机不允许主动发起对SDA的控制，只有在主机发送读取从机的命令后或者从机应答的时候，才能短暂地获取SDA的控制权

这里的开漏输出模式是因为，为了避免SDA总线上，主机和从机同时输出的情况出现，这时候如果一个输出高电平，一个输出低电平，会造成设备短路，这是极力需要避免的，所以为了避免出现一个人向上拉杆子，一个人向下拉杆子的情况出现，就要规定所有人禁止上拉杆子，只能放手或者是下拉杆子，而杆子上方的力使用弹簧来代替，也就是这里的4.7KΩ的弱上拉电阻，如果你要往下拉的话，弹簧肯定是拉不过你的

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTdkY2FiNGZlM2M3OTExZjlhNTkzOWZjNTdjMTg2YjhfTEdMMmFlTlI4djE2M3RjSER0Um41TEdxUTZ5RkFOaHpfVG9rZW46SVFDTWJXc3Myb2J0OHV4QVNnamNaZXBkbndmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

IIC时序基本单元

默认情况下SCL跟SDA默认处于高电平

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2M3ZmIwN2RiZTRjM2JkNzBlZWU0MTNlZGQ0NDMwNGNfRWJUVlRDUmJveUdraGlueHVtNnZvdnRzQXRORjg4amFfVG9rZW46RTFVYWI1UnlCbzdmZUh4U3p0Y2NDZEkwbmZjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

IIC时序单元

主机拉低SCL，把数据放在SDA上 ，主机松开SCl,从机读取SDA的数据，在SCL的同步下，依次进行主机发送和从机接收，循环8次，就发送了8位数据，也就是一个字节，另外注意，这里是高位先行，也就是一个字节的高位B7

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzZmOTQ3ZTA4MTVmOGU5YjQzYzMxMDgyNTA4ZTY1ZTlfYU5XZVBRamlsYzQ5YktTYlFwTVJZVW1YNXlBYVAyNHZfVG9rZW46TldKRGJoZUkzb2p5anl4Z0UzTGNsWEx3bkVmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

接收一个字节

SCL低电平，从机放数据，高电平主机读取数据，可以理解为，默认状态下，主机和从机都处于输入模式，如果想要输出，就要主动拉低SCL，但是如果一直拽着SCL不放，就会影响到从机的发送，因为此时接收到的所有数据都为低电平，

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjNjNDIwMzQzZjg1YTQzNmJhYTNkMmY4NzI0ZDBlOWNfOUFVS3FlUFJMc3dTRXpMYlhvNm9Qd3JjS2RDZVpSZFVfVG9rZW46Q2VnS2JkQUtJb0FMWWV4a2U0OGNNdmJEbkZiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### IIC时序

#### 对于指定地址写

这个波形就是IIC的实际传输波形，当SCK上拉的时候，下拉SDA产生一个开始标志位，下拉SCL进行数据写入，上拉SCL从机读取SDA数据，标头一共会发送一个字节的数据，其中前７位用于确定通讯对象，最后一位用于确认操作读还是操作写，０表示，之后的时许，主机要进行写入的操作，１表示，之后主机要玩完成读取的操作，根据协议要求，紧跟着的就是从机应答位，在这个时刻，主机要释放SDA，这里RA位是０的原因是，虽然主机放开了SDA，但是，由于放开的时候，从机完成了应答，在放下的瞬间，把SDA进行下拉，所以示波器检测到的信号是０，这时候，就说明我进行寻址，有人给我应答了，传输没有问题，如果没有人应答，那么就会直接产生停止条件，并且提示一些信息，如果不需要数据传输了，就会产生停止条件，在停止条件之前，先拉低SDA，为后续的SDA上升沿做准备，然后释放SCL，再去释放SDA，这样就产生了SCL高电平期间，SDA的上升沿，套用下面这句话，这个数据帧的作用就是对于从机11010000地址的设备，进行写入，在其内部的0x19寄存器中，写入0xAA这个数据

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDIwOGRkYjBkNTBiYmM1MTMwM2RlZDRiNGQxMTY5ZTVfblVFa3JJVEVpcjFwWkNLNVFia1F1VG9hbm1xaU54MVJfVG9rZW46U1dxZWJ6aUVZb29CWEt4WDJ5RmM5RDhibjBkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 对于当前地址读

最开始，还是SCL高电平期间，拉低SDA，产生起始条件，起始条件开启后，主机必须首先调用发送一个字节，来进行从机的寻址和指定读写标志位，比如下面图片的波形，表示本次寻址的目标是11010000的设备，同时最后一位标志位为1，表示主机想要读取数据，紧跟着接收一下从机应答位，应答为0，就代表从机接收到了第一个数据，从机应答之后，数据的传输方向就要反过来了，可以看到，当从机应答后的第一个信号，就是数据字节，没有指定寄存器，这就要用到这里说到的地址指针了，在从机里，所有寄存器都被分配到了一个线性的区域中，并且会有一个指针指向相对于的寄存器，这个指针默认上电，一般指向位0地址，并且，每写入一个字节，或是读出一个字节，这个指正就会自动自增依次，自动移动到下一个地址，那么在调用当前地址读的时序时，主机没有指定要读那个寄存器的地址，从机就会返回当前指针指向寄存器的值，这个时序，并不能指定读的地址，所以用的不是很多

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDY4ZjA3OWRkNjNiY2E2MGVhYTQ1ZDJlNmZkNDFiZTVfbFBtQ1Fwb2tYQU01MDl5WEd4SGk1UnBmU3R3NU5vMHdfVG9rZW46RjJwN2JKQzhNb1ZsSGt4Q29hRGM2YVA4blRnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 对于指定地址读

根据上面的原理，当写入操作后，当前地址读的地址就是写入地址的下一位，所以可以把指定地址写，放在前面，指定以后还没有来得及写，就进行当前地址读，这里的0x19代表接收到数据之后，指针就指向了寄存器0x19的地址，之后我们要写入的数据，不给他发，直接再来一个起始条件，这个Sr的意思(Start Repeat),就是重复起始条件，相当于另外启一个时序，因为指定读写标志位只能跟着起始条件的额第一个字节

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmJjZmJiNTEwMjI3MDE5NDUxNGM3N2Y0ODU2NTMzYTFfajMwaElPSEhWMjhDWWFtY1M3Vnd3bUo2YVlCQnpOSFlfVG9rZW46SlU1M2IxZnJTb3djQVV4R2hTUWNGdlU4bkdjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

总结：

暂时无法在飞书文档外展示此内容

### MPU6050

**一、欧拉角介绍**

1. 欧拉角是描述刚体在三维空间中旋转的方法，由偏航角（yaw）、俯仰角（pitch）和滚转角（roll）组成。
2. 偏航角绕 Z 轴旋转，描述物体左右旋转；俯仰角绕 Y 轴旋转，描述物体上下倾斜；滚转角绕 X 轴旋转，描述物体左右倾斜。

**二、加速度计**

1. 加速度计类似弹簧测力计，中间有可滑动小滑块，左右有弹簧顶着，滑块带动电位器滑动，电位器是分压电阻。
2. 根据牛顿第二定律 F=Ma，测量单位质量物体所受力 F 可得加速度 A。
3. 芯片内部为六轴组成正方形，放小球可测三轴向加速度，芯片平放在地球上底面受力加速度为 1g，自由落体时三轴向为 0。
4. 芯片倾斜可通过三角函数求倾角，但仅在静止时准确，因加速度分为重力加速度和运动加速度，运动时会受影响。

**三、陀螺仪传感器**

1. 根据角动量守恒，陀螺仪中心旋转轮高速旋转时具有保持原有角动量趋势，旋转轴方向不变，外部物体转动会在平衡环产生角度偏差。
2. MPU6050 测量角速度而非角度，通过角速度积分可得角度。
3. 角速度积分得到的角度有局限性，物体静止时角速度因噪声无法归零，积分会导致角度缓慢偏移。
4. 陀螺仪动态稳定静态不稳定，加速度计静态稳定动态不稳定，融合可得到静态和动态都稳定的姿态角。

#### MPU6050参数

16位ADC采集传感器的模拟信号，量化范围：

加速度计满量程的选择：

陀螺仪满量程的选择

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTg4YmI2MGVlYjE5ZWI2ZmRkZmVhYmJhYzBmZDkzM2VfUmZielF3NlZzd0RIQm93S1RaSnRDVDh2cmJoTnhzMm5fVG9rZW46U0t2amJ4TzhMbzdWSHZ4WmJsUmNWMENwbmhoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 硬件电路

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Mzg1OTEzNjlkNDgxZTU1NDA5NmMwOThlZmFhYWI3ZGZfWjN2MWFQbmR1WUFmZFk4YkNXc3luNUNhWGlvejAwcDVfVG9rZW46RnN5QmJrcUVCb25nVXJ4d29XS2M1YnpwbmpjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 软件模拟读写MPU6050

这里由于使用的是软件模拟IIC，所以SDA跟SCL接在任意两个普通IO口就可以了，软件iic我们需要完成两个任务，第一个任务，把SCL跟SDA都初始化为开漏输出模式，第二个任务，把SCL跟SDA置为高电平

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTFmNGYyYmU2NzcxZDk4YmZlYjA4ODY5YTkxMTRkMjhfZ3JMM1Z2QmRTVkhMSk41RU1YY0xMR2NlVmhqSFJST29fVG9rZW46SEpJb2JPZ0Nxb1ptUTd4MVVsMmNtR3lvblNlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

本质上其实就是一个读写分离的状态，当SCL低电平的时候，进行写入操作，当SCL高电平的时候，执行读取操作，也就是放开之后，默认处于弱上拉的输入状态，所有设备禁止操作，如果你硬要操作，那么就是 起始条件和结束条件，当SCL处于高电平的的时候，SDA下拉，就是起始状态，反之SDA上拉，就是结束条件，这样的差异化，能够在数据传输的时候，快速的进行开始与结束

#### 代码编写分层

有了良好的分层结构，我们在写每一层的时候，就可以专注每一层的测试，其他层的事情就不用管，完成一层之后，就尽量对这一层进行测试，测试通过了，再进行后续的代码

暂时无法在飞书文档外展示此内容

### STM32IIC外设简介

1. STM32 IIC 外设硬件功能：
   1. 硬件收发器可自动执行时钟生成、起始和终止条件生成、应答位收发、数据收发等功能，通过硬件电路自动反转引脚电平。
   2. 软件通过写入控制寄存器 CR 和数据寄存器 DR 实现协议，读取状态寄存器 SR 了解当前寄存器状态。如开车时，CR 像控制方向，SR 像看仪表盘。
   3. 存储器存储数据，寄存器与硬件电路挂钩，可直接操作电路。有硬件外设可减少 CPU 负担，增加效率。
2. 固定多主机模式：
   1. 正常一主多从模式下，主机有绝对控制权，从机需主机允许才能操作总线。
   2. 固定多主机模式下，总线上有两个或多个主机，部分时钟固定为主机，部分为从机。类似教室中多位老师和学生，老师可控制学生，两个老师同时说话会进行仲裁，失败方让出总线控制权。
3. 可变多主机模式：
   1. 总线上无固定主机或从机，总线空闲时任何人可充当主机，通讯完成后让出总线控制权回到从机位置。
   2. STM32 的 IIC 外设按此模式设计，需按 “谁要做主机，谁就跳出来” 的思路操作。
4. 7 位地址与 10 位地址：
   1. 7 位地址下最大只有 128 种地址，若设备超过 128 或有地址冲突，可通过配置地址低位、开辟新总线或在协议上分配更多地址解决。
   2. STM32 的 IIC 总线支持 10 位地址模式，最多有 1024 种地址。实现方式是起始后的前两个字节都是寻址地址，前五位为标志位（11110）代表这是 10 位地址。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=M2ZkMGJkNGYwZDNiYTViYjY2NTc4MTE2MDVmNmU0ODJfdTZESDgwaUpFT1NmakplQ1dvMVBtb0locnNBQ29TeXdfVG9rZW46RzJIc2JlMVY4b2R1aHZ4MmtZWGN2cDNKbm9iXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### IIC框图

1. SDA 和 SCL 引脚及数据传输：
   1. SDA 引脚负责数据控制，包含数据寄存器和数据移位寄存器。
   2. 数据寄存器在移位寄存器无数据时将数据移入移位寄存器，新数据自动放入数据寄存器，移位寄存器转运数据时置状态寄存器 TXE 为 1，表示发送寄存器为空，进入下一轮循环。
   3. 接收数据时，数据从 SDA 引脚进入移位寄存器后移动到接收寄存器，同时置 RXNE 标志位表示接收寄存器非空，可从数据寄存器读取数据，与串口收发类似，区别在于全双工和半双工。发送 / 读取需写入控制状态寄存器对应位操作，起始、终止、应答位等由控制电路完成。
2. STM32 作为从机：
   1. STM32 作为从机时需从机地址，由自身地址寄存器决定。当主机寻址发现与 STM32 自身地址或双地址寄存器中的地址相同时，STM32 作为从机响应外部主机召唤，支持同时响应两个地址，需在多主机模型下理解。
3. 数据校验模块：
   1. 发送多字节数据帧时，硬件可自动完成 CRC 校验计算，根据前面数据进行运算得到一个字节校验位附加在数据位后面。
   2. 接收数据后，STM32 硬件可自动执行校验判定，若数据传输出错，CRC 校验不通过，置数据错误标志位。
4. SCL 时钟控制及其他：
   1. SCL 时钟控制可当做黑盒子，写入时钟控制寄存器对应位电路执行对应功能。
   2. 控制逻辑电路通过写入控制寄存器对整个电路进行控制，读取状态寄存器检测电路工作状态。
   3. 内部标志位置 1 可能事件紧急，可进入中断程序处理。
   4. 在进行多字节数据接收时可配合 DMA 提高效率。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MWE4ZDExY2YxNjcyZjExOWMyNDE3OGRlMzE1MTk3NjlfYTNSVVRRSlNsT2Q5NUprMVM4UDFESWtWVktMMGEyVGZfVG9rZW46V3Nrc2I2MUU4bzR0SDB4dmxTT2NmbzlDbndjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### IIC基本结构

在使用IIC外设的时候，这两个GPIO口都要配置为复用开漏输出的模式，复用，就是GPIO的状态是交由片上外设来进行控制的，开漏输出，这是IIC协议的要求端口配置

暂时无法在飞书文档外展示此内容

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDc1Y2QxNTRjYjljY2Q0MDcxNmJmNjZhM2YzNzBhYzBfYjE5TTd0c2JHR0Y0MXdpc01SNUMyelZKemJid25DSXpfVG9rZW46UDE2eGI0Q0pwb2htbGd4YXN0RmM5NkVRbjNlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 主机发送

STM32 的 IIC 主发送分为 7 位主发送和 10 位主发送。

- 7 位主发送时序流程为起始、从机地址、应答、数据 1、应答、数据 2 应答等。
- 10 位寻址模式流程是起始、111100（从机地址 2 位和 1 位读写设置），后面 8 位跟着都是地址。

从头来看，初始化后总线默认空闲状态，STM32 默认是从模式。为产生起始条件，STM32 要写入一个寄存器进行设置，用 EV5 事件表示特定大标志位。当检测到起始条件已发送，就可以发送一个字节的从机地址，将从机地址写入数据寄存器 DR 后，硬件电路会自动把数据放到移位寄存器，再放到 IIC 总线上，之后硬件自动接收应答位进行判断，0 为从机应答，1 为从机未应答。

这整个过程可能看上去比较复杂，操作和事件都比较多，但是简单来说就是，写入控制寄存器CR或是数据寄存器DR，就可以控制时序单元的发生，比如产生起始条件，发送一个字节数据，时序单元发生后，检查相应的EV事件，起始就是检查状态寄存器SR，来等待时序单元发送完成，然后一次按照这个流程

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWQyYmFmM2Y0MzBkNGJlOWJlYzgxNGVjNGY1ZTE2ZmVfcERtemtvbHZxNXhYWHhQQURWSVVrOVhQcW1kSHFMaW9fVG9rZW46U0kydWJkaFEyb2hwZjN4bGM3Q2N0Wmg0bnhjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 主机接收

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NGUxNmU3OTE2YTRkZmQzMDBlODc4MTRmNTBmMDFlYmZfTHZSUGlYdURJOU10ajEyN21VZFBCNnNJUWZSaUh6S1ZfVG9rZW46VDFGaWJhUVYyb3FRYTZ4Y3RoTmNnQnZxbnVkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

####     硬件IIC读写MPU6050

接线图是跟上面的软件读写IIC一致的

# SPI通讯

### SPI通讯简介

**一、SCK 引脚**

1. SCK 引脚用于提供同步时钟信号。
2. 数据的输入输出在 SCK 的上升沿或下降沿产生，能明确确定数据位的收发时刻。
3. 同步时序具有时钟快慢、中途暂停都没问题的好处。

**二、全双工协议**

1. SPI 设备是全双工协议，有两条数据通讯线，MOSI 是主机输出、从机输入线。
2. 主机接在 MOSI 上是主机输出（MO），从机接在 MOSI 上是主机输入（MI）。

**三、与 I2C 的区别**

1. I2C 起始条件后要进行寻址操作，SPI 则开辟 SS 线指定通讯从机。
2. SPI 主机可能有多个从机时会开辟多条 SS 线，低电平表示要找对应的从机，高电平表示不找。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTk0NWUyZTZkM2RlZTk1OGFiZGRjNTE5MWMyNGYwNzdfc1d1YW9KQkNtZmlBeU1hWVJ2ZER1cVdFeEdkOU1nSzRfVG9rZW46VnpKVGJ3N01tb0dQQkx4S3BMQ2MwbFNnbkpmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 硬件电路

**一、确定 MISO 和 MOSI**

1. 根据主机从机身份判断。STM32 为主机时，MOSI 为主机输出、从机输入；MISO 为从机输出、主机输入。
2. 主机和从机的 MISO 与 MISO 相接，MOSI 与 MOSI 相接。

**二、SS 线的作用**

1. SS 可选，所有从机的 SCK 为时钟输入，主机的 SS 为输出，从机的 SS 为输入。
2. 若有多个从机，需要多条 SS 线，SS 是低电平有效。
3. 主机初始化后将所有 SS 线置为高电平，指定从机时把对应 SS 输出线置为低电平。

**三、引脚配置及传输速度**

1. 输出引脚配置为推挽输出，输入引脚配置为浮空或上拉输入。
2. 推挽输出使 SPI 的上升沿和下降沿迅速，不像 I2C 上升沿缓慢，SPI 传输速度一般能达到 MHz。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzQ4ODA4Y2VkYzk0MjYxOTc4NDZkZmJhZmQ0MzU4NTVfWkl0cUNSN1lqY3A1dUVpT1Nsc3FuNjhTZ1ZQT1pFbGlfVG9rZW46SGxUWmJOUjREb2pUUFB4U2FSemNjNjJlbldoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

移位示意图

暂时无法在飞书文档外展示此内容

SPI通讯的基础，就是交换字节，有了交换一个字节，就可以实现交换一个字节，接收一个字节，以及交换一个字节，那么如何实现只接收/发送呢，只需要在不要的数据那里，发送一个0x00或者是0xff就可以了，不需要读取。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDc3YjJlODM3MjVhZmQ1M2Y4ZGVkZTNjMGJkZGM1OWVfU1VSNWZSTUh1VWRqVnBpQUpsN2lET0FKVU1zWm9wV3dfVG9rZW46T1FCeGJjZWZob2NpV2d4ZEpmb2NBZWdmbnhzXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### SPI基本时序单元

#### 起始条件/终止条件

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTk0N2VlN2Y3OGIxNGFkYWJmYzc5Y2NhMzMzOTc0ZTNfWmpKTkdaNWYzTmc2TWExU3Q5d2RZaHJUeVlBeDdHc0RfVG9rZW46UUQzM2JHNEhYbzZ0Unl4NVptcmM4T0lobjNnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

SPI CLK时钟上升沿/下降沿所执行的操作并没有定死，这样可以兼容更多的芯片，在这里CPOL每一位可以配置为1或者0，总共下来就有模式0、1、2、3这4种模式，这里的CPHA决定的是第一个时钟采样移入，还是第二个时钟采样移入，并不是规定上升沿采样还是下降沿采样，而这里的CPOL，是决定空闲状态的时候，CLK为高电平还是低电平，是决定时钟极性的参数

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=M2NjZmVkYzJkZjgzZTE5YTcxYjYwYjg4NzNmMjdjM2Rfdk9QYVNySkRZTFUzdVFibkhCMWkyRlVOMnN6Y3FjaEZfVG9rZW46RFVhOGJDMHdPb29JeEZ4aER6Z2NSNHFVbldoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 指定地址写

首先SS下降沿，开始时序，这里MOSI空闲的时候，是高电平，所以在下降沿之后，SCK第一个时钟之前，MOSI变换数据，由高电平变化为低电平，然后SCK上升沿，数据采样输入，后面还是一样哈，上升沿采样数据，下降沿变换数据

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWY2MzE0N2Q5ZDI1M2FiNGExM2UxNjliNDMzNzUwMzdfYWVMdE9ick52U2lEZ2dpMVVScDIxWnF0c2lxRVhod3FfVG9rZW46SnBkM2JQcTI4b2FxOFJ4amFGbGM1Q091bnFjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### W25Q64

#### W25Q64简单介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWNkNThlMzgyN2Q0MGI5ZTA4MDgyNzFiZmQ5NTgwMzdfVmRrVGlzNm5wZ0JFbGtMRVl4WjB4Wk9xNVN3ak90a2RfVG9rZW46VEQwUWJNYnR6b3ZINjV4aXZ0S2NGVlp6bk1nXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

**一、整体存储划分概述**

1. W25Q64 容量为 8MByte，为便于管理进行划分。
2. 常见划分方式为：先划分为若干块（Block），每块再划分为若干扇区（Sector），每个扇区又可分为很多页（Page）。

**二、地址范围及特点**

1. 地址宽度为 24 位，以字节为单位，每个字节有唯一地址，起始地址为 00 00 00h，结束地址为 7F FF FFh。因 24 位地址最大寻址范围是 16MB，而芯片为 8MB，所以最后一个字节以 7F 开头。

**三、块（Block）划分**

1. 以每 64KB 为一个单元划分为块，从块 0 开始依次往后，共 128 块。
   1. 块 0 的起始地址为 00 00 00，结束地址为 00 FF FF。
   2. 块 31 的起始地址为 1F 00 00，结束地址为 1F FF FF。每一块内地址变化范围是低位的 2 个字节。

**四、扇区（Sector）划分**

1. 每一块以 4KB 为一份划分为扇区，每块有 16 个扇区，从扇区 0 到扇区 15。

**五、写入数据划分**

1. 写入数据时以更小的范围页进行划分。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWVhMjVmMWYxMjljZjk3MTUyYmEzMDlmNDJmMjA0MDRfU0dCQlVBVkFDNVhma2d6TG1kV2hSV2tadFJvUnVybUFfVG9rZW46SWpYZWJWR3Zjb2RtdWJ4NG5jWmM5a2Zqbm1HXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

暂时无法在飞书文档外展示此内容

#### Flash操作注意事项

因为Flash不像SRAM那样，他是非易失性存储器，为了这个特定，就要在写入操作简易程度上做出让步，SRAM是可以直接写入并且数据覆盖的

因为每个数据位只能由1改写为0，不能由0改写为1的特性，所以要对Flash内部进行数据更改，就需要对Flash进行擦除，这里引入擦除的概念，擦除会有专门的擦除电路进行擦除，这样就可以弥补第二条的限制了

擦除的时候，有着最小擦除单元的限制，最小擦除单元为一个扇区，也就是4MB，说明你要是想单独擦除一个字节，就需要将那个字节所在扇区全部擦除

连续写入多个字节的时候，最大可以写入一页的数据，也就是如果你从SRM中间的地址开始写，写入256字节的数据，那么剩下的数据，就会从头覆盖到开头

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDk4MWRjZGE3ZjgxOGI2OGJkM2IyMDFlZGE0MzM1YjZfRVRMYkhaY2V0bENIZjZQN245bzZyZDlUNDVCQXRoZzNfVG9rZW46SlRBdmJva0Z6b0lwQUN4amRaYWNJdGpYbmNiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 软件模拟SPI读写W25Q64

首先我们进行一下代码规划，在这里，跟上一章节的I2C程序差不多

暂时无法在飞书文档外展示此内容

#### 硬件实现SPI读写W25Q64

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTczMzllNTBmNWFlYzJjZDgyYWNkZmIzODA1NzgxYzdfNzh3TnZXM2Q3dEtEYmhNczVFdlFKaGdhSm01UGFkOWhfVG9rZW46TERHWWIxek82b2oxVWp4SVI4TWNGNWxOblpiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### SPI框图

左上角这里，就是数据寄存器与移位寄存器打配合，设计思路与I2C、串口通讯有异曲同工之妙，主要是为了实现连续的数据流，

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTliZmRiNzc4MTQ4N2VkMjQyYTI0OGRlYTQ4ZTBlNTVfTHNmbGw1cEdJQ1lwRFowaE9XS2F5TTJVRXhkbktHYUxfVG9rZW46UjAxbmJ4VUE5b0dobll4bVRMc2NDSVp0bkViXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### SPI基本结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MzdmZTc3YTQ5ZTkwMjgzZmU4Y2FkNGYxOGQwN2MwZjBfdFREVk8xb0NyVDk3dXV3UUZKSnVhVXFlalVSWVByaXhfVG9rZW46WUplOGJsaDN6b0k2dld4clVMOGNwZmllbmRjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 主模式全双工连续传输

1. 选择要与之通信的从设备：
   1. 通过将相应的片选线拉低来选中从设备。
2. 将要发送的数据写入发送寄存器：
   1. 主设备将数据写入 SPI 的发送寄存器，数据会在时钟信号的控制下通过 MOSI 线发送给从设备。
3. 同时，主设备从 MISO 线接收从设备发送的数据：
   1. 接收的数据会被存储在接收寄存器中，可以随时读取。
4. 持续进行数据的发送和接收：
   1. 在连续传输模式下，主设备可以不断地写入发送寄存器和读取接收寄存器，实现连续的数据交换。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OGExYzQzOTE2MDY3YWQ1ZTljMTUxZGYzNDJiNDUyMDlfVWRqS2htbWFHMkdTM2U3djZPS2ZKOHRDbm42ZDV0N3pfVG9rZW46SXRISmJRMzQzbzc0bUh4MWNxWWMwUFRDbnNlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 非连续发送

整体步骤，1.等待TXE为1，2.写入发送的数据至TDR，３.等待RXNE为1，4.读取RDR接收的数据，５.之后交换第二个字节，重复这四步，其实就是等待－＞发送数据 -> 等待 ->接收数据

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MzBiYWFlODRjZjcxMjE4ZDBjYWEwZTY2MDZiNDEwNTVfRGtaU3JZMDdSS2k4cndoZWZBYjNzUjZtWkNPNTRUQkRfVG9rZW46VmtrTGJpTzIwb1hnS2Z4a3JWWWNxd3RibkxnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# CAN总线通讯

1. 线路简洁抗干扰：仅有两根通讯线，为差分信号，无需共地，抗干扰能力强。
2. 多设备连接：可挂载多设备，传输模式为异步半双工。
3. 高效数据传输：报文 ID 可区分功能和决定优先级，一次可发送 8 个字节，有广播式和请求式传输方式。
4. 校验机制可靠：包括应答、CRC 校验、位填充等，即 E2E 校验。

**一、CAN 总线的优势**

1. 线路简洁：仅两根通讯线，采用差分信号传输，无需共地。
2. 抗干扰强：因差分特性，抗干扰能力突出。
3. 多设备适用：可挂载多设备，满足不同场景需求。
4. 数据传输高效：相比串口通讯，可一次发送更多字节。

**二、CAN 总线的传输模式**

1. 异步半双工：保证数据传输稳定可靠。
2. 多种方式：广播式和请求式满足不同需求。

**三、CAN 总线的报文 ID**

1. 功能区分：用于区别消息功能。
2. 优先级决定：ID 号小的优先发送。
3. 标准与扩展：有 11（标准）和 29（扩展）两种。

**四、CAN 总线的校验机制**

1. E2E 校验：确保数据传输准确。
2. 包括应答、CRC 校验、位填充等。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWI0MGNmNDc4ZWFkNjFhYzFmZDNiYmRmZjE5ZTViODdfQXdyZnFHbkZBVEtNbUszUUdKTVp2c0ZlTEY3OW9Gb3JfVG9rZW46RUpBSmJIUTNLb3NHeVd4OWd3cGNyOHp6bmFiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 主流通讯协议对比

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDM3OGZhODcwMDJmNzMwYzVmYWIwY2UzYzJhOGRjODZfRGl0MmN1Skt1OWJHV2owOWJXc2k2VDIxSWRSU2JxR0JfVG9rZW46QmFqeWJDOVhKb2JWNmx4UnVPb2M4TkdYbmNoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## CAN硬件电路

CAN 总线分为高速 CAN 和低速 CAN 两种模式：

一、高速 CAN

1. 使用闭环网络。
2. 每个设备通过 CAN 收发器挂载在总线上，CAN 收发器实现电平转换、输出驱动和输入采样功能。
3. CAN 控制器的 TX 和 RX 与 CAN 收发器相连，CAN 收发器的 CAN_H 和 CAN_L 与总线的 CAN_H 和 CAN_L 相连。
4. 总线走差分信号，用双绞线避免干扰。
5. 在 CAN_H 和 CAN_L 两端添加 120Ω 终端电阻，作用有：
   1. 防止回波反射，尤其在高频信号和远距离传输场景，避免信号波形在线路终端反射干扰原始信号。
   2. 在没有设备工作时将电压收紧，使两根线电压一致，避免电路冲突和短路，实现 “线与特性”，对总线仲裁重要。总线默认状态为 1，数据传输时可快速反转，支持速率较快但功耗较大，发送数据时操作总线呈现 0 状态，不发送数据时终端电阻将总线收紧呈现 1 状态。

二、低速 CAN

1. 使用开环网络。
2. 在 CAN_H 和 CAN_L 的其中一端添加 2.2KΩ 终端电阻，虽电阻另一端未接入电路，但可防止回波反射。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWI3MmUxY2VhY2FkMGQ5MzFkZDUwNWYyNWE0Y2YyZGJfZ0JTa3JxRUdWZHVUYm95TkFEUGVwZmljVTN3ZmNNb3dfVG9rZW46U21PWGJ2cFVhb0ZoQ3B4bzFxU2NjSlNCbmtiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## CAN的电平标准

**高速 CAN**：

- 电压差规定中，0V 表示逻辑 1（隐性电平），2V 表示逻辑 0（显性电平），与通常认知不同。当 CAN_H 和 CAN_L 两线对地电压都为 2.5V 时表示逻辑 0 状态；当 CAN_H 为 3.5V、CAN_L 为 1.5V 时，电压差为 2V，也表示逻辑 0 状态。高速 CAN 总线两边加上闭合的终端电阻有利于总线快速回归隐性电平，从而实现较快的传输速度。

**低速 CAN**：

- 电压差为 -1.5V 时表示逻辑 1，电压差为 3V 时表示逻辑 0。由于低速 CAN 传输距离远，考虑到线路压降提高了压差，使得逻辑 1 和逻辑 0 有明显区别。在逻辑 1 情况下，CAN_H 和 CAN_L 两线电压差不相同，不能像高速 CAN 那样将两条线串联以实现收紧趋势。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODFjOTA2NjZmZDQyOGVjYjlhYjQ1MjNiNTg1ZjJmMThfMTZYVEQ5dGpqMWJVcHVGMlZOSVExbWtLZHdQS3ltd2lfVG9rZW46WDFrTmJKTEVLb2hibUF4TUpkTmNGb0k4bkNjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## CAN收发器

总结来说，如果TXD给1 ，则不会对总线进行任何操作，如果TXD悬空，则默认也是给1，如果TXD给0，则驱动器会把CANH 拉高 CANL拉低，使得两线产生电压差，呈现逻辑0的情况，如果TXD一直给0 出错了，则触发显性超时，收发器会主动释放CAN总线

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Mzk1ZWQ4NTczMWY1ZTg0YzIxMzRhN2U5NjIzNmM1OWNfSHpUSXJGOTJsS1ZsbExOcGM0VHdxY0tWd0hpbzg1WkRfVG9rZW46TXFpQ2JJdlFlb2VTcXJ4NGlVS2NwdDJNbnV2XzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## CAN物理层特性

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2RjMThlZmE3YWY5NWNhODA0YTg0MzNiYmFhYTdkMDJfRnVNRm9QWFUzbE5xUXV2M3JyT1lWWXR5cWY1aHk3dGNfVG9rZW46Wmp4V2JGRnVXb3FrS0p4TFVmV2NhREV6bm1oXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## CAN 帧格式

**一、标准帧**

1. 帧起始（SOF）：由一个显性位表示帧开始。
2. 仲裁场：包括 11 位标识符和远程传输请求位（RTR）。标识符决定了报文的优先级，数值越小优先级越高。
3. 控制场：包含数据长度代码（DLC）等信息，指示数据场的字节长度。
4. 数据场：实际要传输的数据内容，长度由控制场中的 DLC 决定。
5. CRC 场：循环冗余校验码，用于检测传输错误。
6. ACK 场：确认位，接收节点正确接收数据后发送显性位确认。
7. 帧结束（EOF）：由七个隐性位表示帧结束。

**二、扩展帧**

1. 帧起始（SOF）：与标准帧相同。
2. 仲裁场：包括 29 位标识符、替代远程请求位（SRR）、标识扩展位（IDE）和远程传输请求位（RTR）。
3. 控制场、数据场、CRC 场、ACK 场和帧结束（EOF）与标准帧类似。

扩展帧提供了更多的标识符空间，可以支持更多的节点和更复杂的系统。在实际应用中，根据具体需求选择使用标准帧或扩展帧。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTU4ZDZmMThjMTBmYTc3ZWJiMjhmZDRhZDE2OWYxZDlfTThiTjNnejk0alNSVGhGeDBIZU1OM1JMNldrWTJVSGNfVG9rZW46SGhEWGJlWW9ab2tXV0F4ZkNWcGNHYks0bjBnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### CAN数据帧（广播式通讯方式）

数据帧初始的时候，只有标准格式这一种，扩展格式增加了ID位数，能承载更多种类的ID，总结来说就是，我想要设计一个波形承载数据，那么必然就需要数据段进行数据发送，为了控制数据段可以发送几个字节，所以加了DLC用于指定数据段的长度，为了区别这个数据的功能，我又在前面加上了ID号，为了实现广播式，类似于只写，或者是请求式，我要用RTR位进行区分，为了判断数据是否正确传输，我又在后面加上了CRC校验，为了判断是否有接收方，我又加上了应答设计，之后R0跟R1是我留的保留位，为了后续升级，之后，前面加上帧起始，后面加上七位1 的EOF帧结束，这个设计就完成了

扩展格式：这里考虑到对于标准格式的兼容性，在进行仲裁的时候，RTR必须跟在ID位置的后面，虽然这里原来的RTR位空了出来，但还是必须给1 ，之后就是IDE了，这一位就是扩展格式标志位了，标准格式中，IDE为显性0，扩展格式中，IDE为隐性1，当接收方收到了一串波形，就会根据IDE位的数据，按照不同的格式进行分析

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjlhOGU5MmMyOThlZDMwNDhhYzA3NTgzYjE5ZjNkNmZfR2IzYjVjeGg4cEU3QUllTWR2RkxCd3hsZkpqdlRuSHFfVG9rZW46WG9JaGJ0WHVlb1ZCTEV4R1VvTmM0VVBxbjBlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 数据帧的各部分用途简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NGFhOWMwOGE3NzhjMzNhNzBmYzdjMTllZjMyMTNiNTRfRkpnQk9xWWdzOEFuWjRFZ3VkeWlBTldFUGE0NUtkYWVfVG9rZW46SmNybmJvbVcyb2pSQjd4Tmg3SmNNbGF0bndiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### CAN数据帧的发展历史

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Mjk1ZTFiOGUwNzFjOGQ4Njc1YmI1OWI1MzU3YTBiYWZfSTVtTnlBd1ByRjRaQ2dVWmtpcm9mZ0NVQ3FNUU5xTW5fVG9rZW46Q1VpOWJJT2Jvb1VHZEx4VmsxR2Mwc2E2bnNiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 遥控帧

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2JlMTYxNzhiNWRmNGIyNzU0YWY2MDI5OGY5Y2UzNTVfUjk0cUNhS1BTbUZjRUNkanZZeVVUanVhYUVva29nT1JfVG9rZW46TGZRN2JiSXI2b2lkcnR4aHFxdmNBYXp5bjZkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 错误帧

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MWQ1YmYzNzg3MjgxNDQ3ZTAxYmYwMjcyNDAyZjU2OGZfQzNqVGxVMDM5OEowdUg1SDFRN2lsRVk5Q1B4T3F2SUlfVG9rZW46V1BEN2JIbVFqb2xLbnl4OHdBamNVaUZ1bkxiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 过载帧

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODIyOTc0MjhlNWM0Njk0ODNjZDMxZGYyNjZiMjZhZjRfRHNxSUtKQ3RjbDFYUDVEaHZDcXJNSFBYcHZzcmYwSUtfVG9rZW46VlJtZmJSeUdNb05JOGt4S3NXeWNmR3Y2blBmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 位填充

位填充的作用，当波形长时间没有变化的时候，强制追加一个相反电平的填充位，有利于接收方根据数据边沿，执行再同步，防止因为时钟等因素的影响，导致接受方不能精准掌握数据采样的时机

第二点就是可以将正常数据流与错误帧、过载帧区别开，因为在错误帧跟过载帧的规定中，是连续发送六个相同的数据

第三点就是，在总线活跃的情况下，防止被误认为总线空闲，其中的规定是，当出现连续11个相同的状态1 时，则判定总线空闲，而有了

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTk3NmI4MDRlNDQzOGI3ZmJkZTJlY2I4YTIwZGY0NTZfVXhtWnlhcFNQdHNKZ3FzRjIzamxFRUtMRndYNXoySXNfVG9rZW46R1pRRWJwM0lqb1Fxbjl4cnVUN2NvbTd6bk5kXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 波形实例分析

1. 在 CAN 总线中，空闲状态下总线为无电压差的隐性状态。
2. SOF 起始位后，首先发送报文 ID，如 0x555 呈现 11 位二进制状态，十六进制转换时 ID 按 3/4/4 划分。
3. RTR 位呈显性 0 表示数据帧。
4. IDE 为显性 0 表示标准数据帧。
5. 保留位 R0 必须为 0，因为在仲裁时 0 优先级更高，可保证当前定义优先级高于以后定义优先级，如标准模式优先级高于扩展模式。
6. 4 位的 DLC 决定数据位有效载荷，当 DLC 为 1 时数据位发送字节数为 1。
7. 数据位如 10101010 表示数据内容为 0xAA，CAN 总线高位先行。
8. CRC 由 CAN 控制器自动生成和接收。
9. CRC 界定符在 ACK 槽之前让发送方释放总线，否则接收方无法应答。
10. ACK 应答位若接收方正确接收数据则将总线拉开呈状态 0。
11. 之后是 ACK 界定符和 EOF 结束位，结束位后总线呈状态 1。 

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTQyYzMwMzljZmZjY2M2NGJkZWFkNzYxMmEzNDc4NDFfV2pPUHJkZXlkR3k3Z0FQRktPbmdPTTE1clFyclFQTTJfVG9rZW46RjA4eWJoV2hDb1lrS094V0dmd2NMR1ZRblFoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 扩展数据帧波形

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MmJlMTk2MGMyYTJjMTcwNGEyZjJlMTkzZmQ3ZjIwZjVfRDAyRGpSSFR6VDBEelB5QkhraWtZdTBvV0JYM01wb2pfVG9rZW46TlpVc2J5SXJCb0pqVXZ4dTNkZ2NhQU52bjFmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 接收方数据采样

之前我们了解到，挂载在CAN总线上的所有设备，默认状态下，都属于接收方，当某一个数据想要发送数据时，他就会广播自己的数据，拉开/释放 总线，使总线产生这样的一段波形，CAN总线没有时钟线，总线上的所有设备，通过约定波特率，确定每一个波特率的时长，就是异步通讯，比如我想要传输速率为1MBps，即 所有设备都认为，一个数据位的位时长是1us，

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTQwNGY5YjBjN2NjMjFlYmZhNWJjMmM2MmZjNzc5NGNfSGRzcFowM0FqbUs1VjVXdUlNMU9jdlJiSVZaVFR4YU9fVG9rZW46WG12SWJaV1RUbzJYUmN4RlJNcWNKQ3JLbjNmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 接收方数据采样遇到的问题

时钟误差&采样点未对其

相应的解决方案 硬同步&再同步

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjE1N2MzZWFjNDllZDlmZTk1NDI0YTdmMzBhNzRlMTNfUVJ4T0MxbjIzd0xmbmdnYTBpUkVPQk9EVDhkdEN6UDFfVG9rZW46QjJiamJsSW51b0M2WEV4bmxnTmNyckRHbjdiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 位时序

1. CAN 总线为灵活调整采样点位置，将每个数据位的时长进行细分，分为同步段 SS、传播时间端 PTS、相位缓冲端 1 PBS1 和相位缓冲段 2 PBS2。
2. 当数据边沿信号处于 SS 位置时，当前设备与波形同步；若跳变沿不在 SS 段，需调整设备位时序。
3. 若边沿信号每次都在同步段，说明设备位时序与波形同步，接收方在 PBS1 和 PBS2 之间采样可得到准确位置。
4. 若跳变沿在 SS 之外，需用硬同步和再同步调整位时序。
5. PTS 规定数据发送、输入输出在总线上产生延迟时间总和的两倍。
6. PTS、PBS1 和 PBS2 共同决定采样点位置。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MmE4YzY1NWUxZTU0ZmUwMzlhYjU4M2U2YTk4MDVjNTdfbEZoN091S2VpWUtGSkx1R2g2Qjd3amFYYUVoSExsdk5fVG9rZW46SjFwd2JTUWZIb1N6UWV4eXZRaWNTODk5bnZoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 硬同步

1. 当收到起始位 SOF 的下降沿时，相当于发送方发出信号。接收方会将字节的 SS 段与发送方保持同步。
2. 硬同步旨在帧的第一个下降沿 SOF 有效，可以理解为初始化同步。
3. 硬同步在 CAN 总线通信中起着重要的作用，确保接收方与发送方在帧起始位置实现同步，为后续的数据传输奠定基础。
4. 通过硬同步，接收方能够快速调整自己的位时序，以适应发送方的信号，从而保证通信的准确性和可靠性。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjRkYzBkZDQ1YjEyNzI0NjJjOWEyYWMwZmU2ZGQ0ZjlfZTFXSGtLSkVuejVyNmJEcmlReHU1cVJzaXdud2Q2RGpfVG9rZW46WDZNVGJYVnlyb0hGWUN4MWFMa2NyZ09jblpjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 再同步

经过硬同步的初始同步之后，秒表转啊转，时间久了，又有可能出现偏差的问题，偏移多了就会出现接收错误的情况出现

当数据的跳变沿出现在同步段 SS 之外时，接收方根据跳变沿与 SS 的位置关系进行调整。如果跳变沿超前于 SS，接收方会缩短相位缓冲段 1（PBS1），延长相位缓冲段 2（PBS2）；如果跳变沿滞后于 SS，接收方则会延长 PBS1，缩短 PBS2。通过这种方式来调整当前设备的位时序，使得采样点能够靠近数据位中心附近，从而保证数据的准确采样。总结来说，就是通过改变PBS1 跟 PBS2，改变采样位置，从而影响下一次同步帧的位置

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWJlZjg2MzBhZWViYzBjNzAwNDM2ZjM4MjYzMWE4NWNfeWhmdnNLbEZjYlVadFhuVjUyVkNlZnpCMTVqUzFER2FfVG9rZW46UUhXaWJ0a1EwbzE3akt4WU0yVmMwaTFPbnVlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 波特率计算

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OGYxMDFkZDYxYzNiYzQ4ZjhmOTAwODhjNTg1MDY3YzBfbzd3NzQ0OXY4a2RYMG1IVnZDc05IVzlOQ0hRU1J6T05fVG9rZW46VjlodGJ2ZU5KbzVtMGp4Nk5Rd2Mwb0N3bjZkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 总线仲裁

看一下这个波形，这里展示了两个波形，比如说一个设备A，想要发出一个数据帧，所以设备A跳出来，变成发送方，依次拉开或释放总线，使得总线变成上面这样的波形，但是，设备A发出这样一段波形，是需要持续一段时间的，但如果此时，设备B想要发送出另一段波形，这会产生什么现象呢，如果我们对此放任不管的话，那么总线上的波形，其实是二者波形进行“线与”的叠加，这里引入一个概念：线与 即 只要有一个设备拉开总线，总线就会呈现0的状态，只有所有设备都释放总线，总线才会呈现隐性1的状态，那么按照线与特性进行数据叠加之后，那么显然，两个波形都会产生数据损坏

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDJiZmNmMDRhNzIzZDExNzFiNmUwYmZiM2NkZDRmMmFfWG5xVVVIZWlncnNURE9vNDNnbDluNTRtZFE0bWlUcTBfVG9rZW46UjNPNWJYQlNpb0hnUlB4aTBQaWNTY25WbnRlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 解决方法

#### 资源分配规则1 先占先得 

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDg4NjBjYjFhN2RjZjA1NzQxMGVlY2EzMWJkMGFmMWZfUmN3QzdUc3lWdzd3bkhTNGtFUmh2Z0JhT1RSQWpCRnBfVG9rZW46S3l6eWJrNVBRbzI5T0h4M0RRN2N1dFBibjJlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 资源分配规则2 -非破坏性仲裁

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjBjYjRjMDk5NWMzNDIwODY1YTE4NDVhZjk4ZThhYTlfczJoUFBHSVExbEo1QmNnbFl1ZGVHR2R1Zm9yeVp5WTFfVG9rZW46QTY0UmJwd0xBb3FhUDN4clBrbmN2QUY4bjJlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 非破坏性仲裁过程

1. 单元 1 和单元 2 的波形并非绝对同时开始，而是多个设备在上一设备完成数据发送后等待并尝试发送数据，从而产生非破坏性仲裁。
2. 起始位 SOF，单元 1 和单元 2 都发 0，根据线与特性总线为 0，回读正确后继续发送。
3. 发送 ID 号过程中，相同位继续发送，直到最后一位单元 1 发 1、单元 2 发 0，单元 2 仲裁获胜且不破坏数据特性。
4. 单元 2 继续发送数据，采用发送一位读写一位的方式，仅在仲裁段发送与读取数据不同时停止。
5. 填充位前必然执行总线仲裁，若填充位前数据相同则填充位也相同，（填充位是指连续出现五个相同数据时，下一位数据自动补充为相反数据）。
6. 从胜利一方角度看，发送与读取数据相同，感受不到竞争者存在，此为非破坏性仲裁原因。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjA1Zjk3YTI2YTlkZDBiMjBmMGNmOWM5NjVhZGRlNDVfdWtyb2txRTVhMEw0czdDODFOS3VCQVRUenVnRlh5bWNfVG9rZW46WVRNNGJ3ZDQyb3ZWclp4NHg3WWNSRmlMbnRjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 数据帧和遥控帧的优先级

这里有一个前提，数据帧和遥控帧的ID号一样的时候，数据帧的优先级高于遥控帧，比如设备1 发送一个遥控帧，表示想要请求一个ID号的数据帧，而这时候，B设备正好也要发出这个ID号的数据帧，那么就会出现相同ID号的数据帧与遥控帧出现仲裁的情况，当然，相同ID号的数据帧和数据帧，是不允许同时出现的，相同ID的遥控帧和遥控帧也是不能同时出现的，因为他们的位置都一样，就没有办法判断谁先谁后了，这里的优先级仲裁也是符合常识的，因为在请求帧和数据发送同时出现的时候，肯定需要让数据先星，这时候，就由仲裁段的最后一位RTR进行判决，请求帧为1 ，数据帧则为0

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWM3MTBlYjIzYTk1Y2E1YjRiMjJiYTM4ZTY0MzAyNDNfclgwZmNDYjh3TUJLYXppcUZmdEUyTXRtMWZVOTBDaTRfVG9rZW46UTJ6SWJjODBtb1NKOVl4am9zUGNlcnVvbjFkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 标准格式和扩展格式的优先级

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Mjg0ZGRkNGJkNjVjN2YyZDgzNjdhMDdkYWU0MDI1YTlfdE1HeGJVSlRrZUZVUXFLVm9sMGN5Q1VFWlBJUmhsN1lfVG9rZW46UlNOVGJaaHFLb2hRNW14NjlHSGNNbzlSbjdjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 错误处理机制

1. 位错误：依靠回读机制检测，设备发送位后采样，不一致则为位错误，可能在仲裁段仲裁失利或接收应答时接收方反馈。
2. 填充错误：数据填充不正确会引发填充错误，影响通信正常进行，需严格按照规范填充数据。
3. CRC 错误：仅接收单元检测，通过对数据计算校验码，不一致则说明数据传输有错误。
4. 格式错误：数据格式不符规范产生格式错误，可能导致接收方无法正确解析，双方需严格遵守协议规范。
5. ACK 错误：发送方未收到正确 ACK 信号为 ACK 错误，可能因接收方问题或链路故障，影响通信效率和可靠性。

但是目前这个设计有一个风险存在，那就是错误通知赋予了每个设备破坏传输的能力，如果有一个设备抽风了，他无论受到啥，都认为是错误的，本来是正确的，他也认为是错误的，那么这样，总线上正常的数据传输，都无法进行了，所以错误通知还需要加上一些制，来防止这种问题的出现，这里首先复习 一下错误帧，他由6位的错误标志，和8位的错误界定符组成，分为主动错误标志和隐性错误标志两种，主动错误标志是6个隐性0，被动错误标志是6个隐性1

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OGM5MTk3Nzc1M2Q4MDY2MjM1Yzg4ZDkxZmE2YjEzMTNfRWdaQmg3bWxERVprUk5YNWpEdno2M1V0eFJObWxMbHFfVG9rZW46T295dGI1Ym1zb2VMSFJ4MUxhdmNkdENjbnRmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 错误状态

错误状态分别三种，其中，主动错误状态的设备正常参与通讯，并在检测到错误的时候主动发送出错误帧，每个设备初始都为主动错误状态，主动错误的权利是比较大的，可以破坏别的数据，如果这个设备不太可靠，频繁的发送错误数据帧，就给他转到被动错误，被动错误的设备正常参与通讯，但是检测到错误只能发送被动错误帧，不可以破坏别的数据，如果他在被动错误状态，还在频繁报告错误，就给他转到总线关闭状态，总线关闭状态的设备，不能参与通讯

那么他们判定的标准是什么呢，每个设备内部管理一个TEC跟REC 根据TEC和REC的数值，来确定自己的状态，设备在发送的时候，每次发现一个错误，这个TEC就会增加一次，那么相对的，每正常接收一次，TEC也会减少一次，REC也是同理，如果正常接收没有多少次，错误反倒一堆，那么REC肯定会迅速增加，如果只是偶尔报告一些错误，那么在TEC跟REC增加之后，肯定会迅速减回来，所以根据他们值的大小，就可以判断当前设备是不是可靠

 具体判定可以见下图，但是这里只有在设备出现错误状态，还总想发送数据，并且发送的数据还总是出错的时候，才会把它转到关闭状态

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2JmYTUwZjcwOTYzYWM0NjA3ZjA5OTIwYjMyZTdjOGNfbXYwN2tQU0dOU0xNMGlTb3FHRHhEZkk0cUpGcDJRckVfVG9rZW46TTNFWWIySjdVb2VzOEJ4dTc0amNHeEtEbk9kXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 错误计数器

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2MxZjRiNmQ1ZjhjMWIwY2ZmYmQzNzNkOGNlZmEyYzhfaTM3SEIyRnZOZXI2dVAxeXBVSzIxNDNBTU91Q0VIUXlfVG9rZW46UjVKMWJMT3Vmb0dhWmd4VEk3N2NKTnZNbmZoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## STM32 CAN外设简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDA1YjgzM2QzNDVlODg5NGU2NDQ1MzdhYzZlZTEyNWVfT29BOUNRSlo1UlVGQTVnVVJVRUg0WTFJREMxMjA5ZUdfVG9rZW46RkVSRGJ1Rmppb3FkUjN4ZGxiN2NpaERNbmZlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### CAN网拓扑结构

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODE0ODYxNWNjOTgxODIzOWRmMzBmN2EwYWM4OTgyNWZfQnU0UWhqQ253dkh3cmxvcUdEMjREU1pPMEdscWhSeFRfVG9rZW46RklPZ2JrNGJnb0tiOEt4WG5GbGMwUUVTbkZnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### CAN收发器电路

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjQxZjRmNjNjZmMyNmM5NzlhYjhiZTFmYTA5NjY1OGNfY0FwZUV1bEFzb2V5MTltUXB5VGhWNElKaFdmRDgwbTJfVG9rZW46VHgwN2JkbEVWb1Vldzl4UmdBMmNsUDR3blljXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### CAN框图

1. CAN 框图总体分为主 CAN（CAN1）和 CAN2 两部分，只有互联型设备才有 CAN2。
2. CAN1 和 CAN2 并非单独资源，CAN2 辅助 CAN1 工作。
3. CAN1 的主动核心在 CAN2.0B 的主动核心部分，通过寄存器操作可对电路进行操作。
4. 主发送邮箱每个可存入一个 CAN 报文，发送时将报文写入空置邮箱并设置寄存器即可，后续操作由电路自动完成。
5. 接收部分包括接收过滤器和两个 FIFO（先进先出寄存器，可理解为排队），当 CAN 总线上出现数据帧或遥控帧时，硬件电路自动过滤报文 ID，若为接收方所需数据则放入 FIFO0 或 FIFO1 排队。
6. 每个 FIFO 有三个邮箱，可容纳三个报文，在接收报文快而 CPU 无法及时读取时，可避免数据丢失。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2RiMTBjN2VhMDdhZjkxY2RkMTNkM2RjMTEyN2ZiYTZfRDIxNzY0a3FaZkFqR0JlZVJycmxlVXJKYklvTndSbUpfVG9rZW46TXh6MmI4bDRtb1d3RWR4VU9hTWM3NkNNbnB5XzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### CAN基本结构

1. CAN_TX 和 CAN_RX 信号进来后，首先要对 GPIO 进行初始化配置。
2. 剩下的任务大部分由发送和接收控制器完成。只需要告诉控制器想要发送 / 接收什么数据。比如接收数据时，控制器会将数据放到过滤器上进行过滤。
3. 这里一共有 14 个过滤器，可以对这些过滤器进行规则设定，将想要的报文 ID 写入过滤器上，经过过滤的数据会放到 FIFO 上面。CPU 只需要读取 FIFO 就能读取到数据。
4. 如果 CPU 一直没有读取数据，导致三个报文都排满了，可以对 FIFO 进行设定，分为锁定和不锁定状态。在锁定状态下，新进来的数据会被舍弃；在不锁定的情况下，新进来的数据会将邮箱 2 的数据进行替换，数据丢失是必然的。
5. 设计两个先进先出寄存器是为了将数据的优先级进行分类，就像食堂排队，老师和学生分开排队。
6. 发送邮箱在总线空闲的时候，发送 / 接收控制器会将数据发送到总线上。虽然有一个邮箱就可以，但设计三个邮箱是为了避免 CPU 长时间等待。当 CPU 想要再次存入邮箱而上次的数据还没有发送出去时，可以将数据放到下一个邮箱进行等待。另外，发送的顺序可以配置，有先到先行以及 ID 号小的先行

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MmJlMmQ2NTA2NGViNjhjMWU5NDllNjM2MGEzOWI0OTFfMGhoOHptdERkb1J5V1N2d1o2czBFVm1mSlRtRG5MZjZfVG9rZW46S0pMOGI1dkROb01LUlJ4Y0RwcmNxRjJObnFkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 发送过程

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YWQ1YzJhZDUyNmRmODJhMjVjYmY4ZGQyOWJjYjA0ZWVfSmpMRTZpRkF1MTNRRXk4V3ZFUzl5QVN2aTVtbGpTalFfVG9rZW46T2daWGJmUjZibzFpR3V4Tjh0cmM5OWJ4blplXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 接收过程

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTUxZjlhZjhkNjY1NzdmZTc4NzVmN2Y1ZTRlMWZhMGZfQk1aS1VLNExjRzNEd1Z5NG83OW9LSkNhRkFUWjhmUGtfVG9rZW46QXhLQ2JzV1drb0ZNZ1p4dFRRTWN3U1hObnpmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 发送和接收配置位

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTlmNzM5YzE4Nzc0YjhjMGJjZjM0NDIwNjIwOGQ3MmNfTmlYVzZiSGdtYnBNT0NaZU5CRHFiMVRlcW9ENlhrOVlfVG9rZW46R1hOT2JOUVJnb1gxOVp4SVE5WWNGNlVJbkdoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 标识符过滤器

1. ID 号等过滤信息会放到 R1 和 R2 两个寄存器里面。通过对 FSC 和 FBMA 两个寄存器进行配置，有四种工作模式。
2. 32 位列表模式是最简单的模式。将想要的 ID 号写入 R1/2 寄存器中，可区分标准 ID 和扩展 ID。若只需要标准 ID，在前 11 位写入，IDE 位置 1，RTR 位用于区分数据帧和遥控帧，32 位寄存器还有一位没用，默认保持 0。在这种模式下，一个过滤器最多只能过滤两个 ID，若项目中只需要过滤标准 ID，会造成资源浪费。
3. 16 位标识符列表模式下，2 个 32 位寄存器会被拆成 4 个 16 位的寄存器。高 11 位存入标准 ID，紧跟着是 RTR 用于过滤数据帧和遥控帧，然后是 IDE，最后还有 3 位写 0 即可。
4. 实际使用中，若有过滤一组 ID 的需求，比如一个传感器有一百个温度探头和 100 个湿度探头，可使用标识符屏蔽模式。只需要高位是 0x1 的数据时，可把 ID 号的低位屏蔽，这样就能拿到 100 个以 0x1 开头的数据。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjdiZjNkZTViYzBmYmUyMWIyMzc4YzcyOThhNTY5M2NfdE94Z1FlMUc2Zkd1TXFIU1NWeTllMDBjZ2V6b0hxeUJfVG9rZW46SW54ZWJRMXdub3AwcE94WmFpbGNLN1VubjVjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 过滤器配置示例

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTI4YTlhNzY2Nzk2MjA5YzBmNjUzMjZkYmFkZTc5NmZfdGRuTFd1SXdOWWJ1UFl6cXExdW5KMXQ3R2hrQlVXQmNfVG9rZW46Q1BreGJQVDRIb0xiZGV4U1ZmUWNMend6blFkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 测试模式

1. CAN 有多种工作模式，其中包括正常模式、静默模式、环回模式和环回静默模式。
2. 在静默模式下，外部引出的 CANTX 引脚和 CANRX 引脚工作方式发生变化。TX 引脚时钟发送 1 相当于什么都没干，RX 引脚始终接收 CAN 总线数据且不会对总线造成影响。
3. 环回模式用于自测试，在内部电路上直接将发送和接收接入，接收可以读取发送的数据，与回读机制直接读取电平有本质区别。
4. 环回静默模式将内部的发送和接收直接相连，实现自发自收，同时隔绝外部联系。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTY0ZmVkZjQ2NzM4OGM1MjgwMGE2YjIxOWNlZWUwYTFfcmhKV3BsdU01OFFMSVd5NkJRZkVlMmgzaWdqUmdnWXlfVG9rZW46QlAzcGJWMk1vbzZZRlh4bktya2N0RFlGbjJmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 工作模式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NWY0MGUzZmRkYzZkYTE5MmNlMTg1M2Q4MmJhM2JiNTJfRmtKa2tzNkg0NXpPa0tRYmdUZEtjY1RQWVd4MWZZa3RfVG9rZW46VUtSNGJPalc1b0EyelN4dXJmd2NrY2VkblBlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 位时间特性

波特率 = 时钟频率 / 分频系数 / 一位 TQ 的数量

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MmNjNjU3OTk1N2U1MzBlMzBkN2IxZDNkMmE5NmUwNmVfWUpycE1mUElLRHlyeDlzVTJXNUR2bEowM200Zm90OE9fVG9rZW46VnRYUWI2MkZKb1J4NVJ4aTBoaWNzWEZJbkpjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 中断

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDJmZjc3YTcwYzY5YjU2MDczOTgwNzRmY2NjM2IwZGRfNTZneWNKMzZORUN4dmJhaU1yQlJSMmpidzU0ZnR6dzBfVG9rZW46WllFd2JJdVJsb2RCb1R4dW8xY2NzdUJYblhnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 时间触发通信

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTU5ZjdhMzI3ZDMwYTRjZWI3YTU4NzhkNzcyYzkzYTdfZDBPZ1VqUFplZ1UyY1c2ZVBhUTFaM3Y1dE1ZMGc3MktfVG9rZW46QXQ5c2JWSU1lb3g1dW94RUtiWGNmOVg3bkZkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 错误处理和离线恢复

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YmZkNTA4ZjM0YzI2YjljMDY5NjFlYTlmYjhlNjJlOWZfVUg4OWlmb3c5SnJERGxyQXdrWXkwdjUwdkRCeUNHV2xfVG9rZW46VnN6UmJXZW93b2JPSjZ4UVExcmNoT21jbnhlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# Unix时间戳

nix 时间戳是一种从 1970 年 1 月 1 日 00:00:00 UTC 到特定时间的秒数的时间表示方式。在编程中经常被用到，比如记录事件发生的时间。对于硬件电路来说非常友好，因为计数简单方便，在人类需要读取时，再转换成日期格式即可，无需考虑年月日寄存器、进位、大月小月、平年闰年等问题。其次，在进行时间间隔计算时也非常方便，例如计算 1 月 1 号 8 点到 3 月 1 号 18 点之间间隔多少小时，如果通过年月日记时，需要考虑的因素较多。总的来说，Unix 时间戳在编程和硬件电路中有诸多优势。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTE2NTEwYmY5M2Y0MmQ2M2YwZGE1ZTg5YWIwYmVmY2JfZTRHTjd3U0RVVjNoR3NIM1RZd0k2MW5HNmhGTkoyN0NfVG9rZW46SE5hdWJrbEczb0xwSGp4dmthUGMwZGVZbkhiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## UTC/GMT

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDE4MDEwMThlNmFmOGJjYmM0ZDQyZjA0ZTcyNTQ5NjZfWkpWaFFaM1hSSEZPR0dwekxiS01nQ2xIaWVNd2ZTVUtfVG9rZW46RzBRdmJOTURrb0d5Nk94ejRZU2NwNWNXbnloXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 时间戳转换

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YWU0ODNjM2ExMzdlMGEyY2I3OWEwYTU2NDVlMzM5MTFfS09vNmV6T1dwSU9yZWc1ZEthdEh6aGxIVFhOeWptd2VfVG9rZW46TGZqeGJIZ3Zyb3c1Y3N4WHN2OWM3THVpbkplXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

`gmtime`函数将时间戳转换为 UTC（世界协调时）的时间结构。

`localtime`函数将时间戳转换为本地时间的时间结构。

`mktime`函数则是将一个本地时间结构转换为时间戳。

下面的函数则用于将日期转换为字符串类型显示，strftime 用于显示指定格式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MWQ5NTIxNGFlMGQ3NGU4NDRiYTFiZjM3MDc0MjFhZjhfa28wTHdzYW55ZVpXc1V6R3Qzc0twR3RLN0dNQm5ORHFfVG9rZW46UWRsemJMS3J3bzNKT3B4YWpzUmNWOE84bmcwXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### BKP简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjljZjg4ZmU3ZGM1OWM0NjhhN2E2N2RjMWIwYjM0MmFfcU5WRDNDdGVvcEdJRHdaUTBnN2R5S1pUU3RoT3Rva21fVG9rZW46RG1hamI5TjhMb3FtVzJ4TVJBMmN0TVN2bktoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTdjMGZhNDJkYzUxMmI0N2JhYmQ5YmQ5NWM3YWVmYjFfOXZJQXlDUWY1NGV4R0tJTm1zT29BNHZua0hTb2ZFdDVfVG9rZW46U3FJc2JlcVllb3VpSTZ4RGhXaWNtV2VDbmRoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### RTC介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjZkM2ZmZjRmMzg5NDgyMjg5ZjJlYjFhZDQ1MmJhMDFfNDU2bEl3MldvZUFtdXJlcTBjclE0b0VVV0pDY1ptcFNfVG9rZW46VVd0WGJzQW94bzU5Vkh4SmEybGNWeDFNbmRjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### RTC框图

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDZkYjBhZjBiZmI1NGNhYWIyYzMzNWRmY2YzM2E1MzVfeTQzMFg2TUo5dnIzOXJ6RTFORVc4YW5WQjI1SkpCU3JfVG9rZW46Q2g0WWJ3Q1hBb2pnUXd4RXcwa2NUZ1lVblZnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### RTC基本结构

最左边是RTCCLK时钟来源，这一块需要在RCC里面进行配置，三个时钟选择一个，当做RTCCLK，之后先经过预分频器进行分频，余数寄存器是一个自减计数器，存储当前计数值， 重装寄存器是计数目标，决定分频值，分频之后得到1Hz的秒计数信号，通向32位的秒计数器，1秒自增一次，下面还有一个32位的闹钟值，可以设定闹钟，如果不需要闹钟的话下面这块可以不用管，需要中断的话，就先允许中断，再通向NVIC

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTlmZTM5MGQwMjQ4OWIyMjBjNTE2ZWYzN2EyZDdmMzdfZmRkbjNzZlNZRVg5TDhXNEF5ZjR3YlBrRXBwSm85eDdfVG9rZW46Q3ZscWJYTjlFb0dmd0Z4WnFCbGNaUEFWbkRlXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 硬件电路

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjMzMTAxZmUxYzc3NDRjMTkyN2QzODBiNDAxYWQ4YTRfZnhiWm9VSnpSa25sdFU5QnJxc05DMmdiNEIxWXlnTEpfVG9rZW46SDBUNmJtSFlnb0NlZWd4NnN3WmNDZExnbnpkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### RTC操作注意事项

如果你要开启RTC跟BKP时钟，那么首先要设置RCC_APB1ENR的PWREN和BKPEN，使能PWR和BKP时钟2.设置PWR_CR的DBP，使能对BKP和RTC的访问

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YmVmMDg1NGRlZWI3ODQ0Y2E1OTE2MWNiNmE0NTA0ODZfU01EbXRZcDR3N2Z4RzQ1ZlpkaXpKNHRWV1k3Y2Q5em1fVG9rZW46QkVaUWI4T0J1b1FSZU14MkpRN2N5MHhTbkdnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# PWR电源控制

## PWR简单介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjM0MTUwNWU0ZjdkMTFhOGVhNjhkZjcxZGE5N2ViNjJfbEFkNXIxbVlXMU1NM0EyRDg1b1EzVE93TFpSZjRIdk9fVG9rZW46SDduV2JXNThQb3dNbGZ4MXlZNmNTbW9nbjljXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 电源框图

这个图就是STM32的内部供电方案，其中有些部分，我们之前也已经了解过了，现在再来看看，整体上，这个图可以分成三个部分，最上面是模拟供电部分，叫做VDDA，中间是数字供电部分，包括两块区域，VDD供电区域和1.8V供电区域，下面是后备供电，叫做VBAT，不难发现，STM32 内部供电基本上都是1.8V，当这些电路需要与外部电路进行交流的时候，才会通过IO电路转换到3.3V,所以我们从外部看,好像STM32 所有都是3.3v ，但是实际上，他内部的CPU，外设等，都是1.8V供电运行，使用低电压的主要目的是降低功耗，电压越低，内部电路运行的功耗，就相对越低

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTBjMzU1MjUxMzU2OGFiMzc2NmY2ZjkzZTQ3ZWZhZDFfMm9DZjBvZWU4MkwzZ2ZMdkl2b3pRVVFOWVA1VDRKUU1fVG9rZW46SHV1QWJLUWExb0Z4NDJ4MHFpU2NqTVpwbnllXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 低功耗模式

1. WFI（Wait For Interrupt）是等待中断事件来唤醒处理器继续执行程序，任何中断事件触发，芯片都会立刻醒来。
2. WFE（Wait For Event）是等待事件，唤醒条件是外部中断配置为事件模式或使能中断但未配置 NVIC，产生唤醒事件后芯片会立刻醒来且一般不需要进入中断函数，直接从睡眠处继续运行。
3. WFI 和 WFE 的相同点是调用任意一个后芯片都进入睡眠；不同点是 WFI 需中断唤醒，WFE 需事件唤醒。睡眠对电路的影响是只关 CPU 时钟，对其他电路无操作，电压调节器是 1.8V 区域电源，若关闭在省电评级上为 “一般省电”。
4. 进入停机条件：SLEEPDEEP 位设置为 1 进入深度睡眠模式；PDDS=0 进入停机模式；LPDS 设定电压调节器状态，LPDS=0 电压调节器开启；设置好这些位后调用 WFI 或 WFE 芯片进入停止模式。停止模式的唤醒条件是任何外部中断，在省电评级上为 “非常省电”。
5. 待机模式相当于关闭能关闭的部分，只保留用于唤醒的部分电路时钟，在省电评级上为 “极为省电”。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTliY2Q2MTkzNjA4NTg1NDBmOTA0ZGQxMmZkNzdkMjRfWVR5bnM2VTBVc3ZDMzhFMXhWbEFPcGN5T1RRRko1ZFBfVG9rZW46WkV1eGJuMzJhb1VDSmR4WVJHeWNBZnhjblRoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 模式选择

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDZjNTczYzA3OGM4ZDg0Y2JhZDc2OGVjMzI0ZmRiNzNfMnhFcXh3UzdOQXpVVlVvVVNMczZaZEtpYUU4N08wd1BfVG9rZW46WlpWWmJmbjVjb2x0T0h4a0FyWmNmUFFubjFmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

#### 总结特性

##### 睡眠模式：

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2JjZjA0M2IwMDQyODA2ODYyNmY2MThjN2FiOWI5NThfRjZ4QVhiT3RwbDlHdmRJc1BYMU1wTkhMOWFWbnpJTjdfVG9rZW46QVRpWmJjVkFHb3JHV0x4c1dhMGN2VWFlbjZmXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 停止模式：

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDM3ZmNjOTYzZWU5YzAwYzY4ZjUzYTRlMTQwNjE1ZGNfSGpwaFNSUEV3YWVOTnVITU5hdFFuQ3g1NVVnbDFRUUlfVG9rZW46VW0xaWIxemY4b1dKN2N4dWQ2RmNPQTZmbmRkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

##### 待机模式：

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=M2UyYWZkOGYzZmIxOTcxZGNhODJlMGFjNGJmZjA4MThfVVdYaW1RN0pweUoyc2hqa1ZQMk1ZZzUyOHVmeWhQZTdfVG9rZW46VVlSWmJLYU9Ob2dQNWx4UzdaN2NieWRYbkdnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

  

# WDG看门狗

1. STM32 内置独立看门狗（IWDG）和窗口看门狗（WWDG）。
2. 看门狗本质是定时器，若程序未在指定时间内执行喂狗操作，会自动产生复位信号。
3. 作用是监控程序运行状态，在程序因各种原因出现卡死或跑飞时及时复位程序，保证系统可靠性和安全性。
4. 独立看门狗独立工作，对时间精度要求低，只有一个最晚喂狗界限。
5. 窗口看门狗需在精确计时窗口起作用，喂狗时间早了，或者是晚了都不行。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDQyNzk2YjFiZTJkOWRiNzA1ZWVlMWE4NWZmZTZjNjhfbTN3ZXRMamZPcHpHVXBnRmlPam5MODgxZjlPZlBkaWxfVG9rZW46VzNHdWJZQ3gzb0RjZkx4YWJVMGNSd2hmbkZkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## Independent Watchdog（独立看门狗）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTJjNjIzMGI0MzNiMzA1NWQ5YzY5YTkzNDEzZDAzNjlfWXRxc0ZaQWJWQmNYelRzYWZiWjhiTWhIUDFqYndRWVNfVG9rZW46UUNWVGJxdGt5b3EwaXN4c3RDdWN2ZWxxblVnXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

IWDG键寄存器

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2EzMmMzY2E2MGM5YjBjZjBjN2JjZThjMDllN2VhOWJfZDdmRFF2U2paNkc3dEp2WFpCVk0zQ2N5YW9OUWF4bm9fVG9rZW46U1l4T2J3NTk0b2E4Sk94Rll4ZWM4ZmJubnFiXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### IWDG超时时间

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTk0ZTM3ZmFlMDhiMDAxMmM5Y2I0OTViZjA2Y2Y5NmVfZWF2QVRhS2JObnI0dzJSTmtMMEtlQmxFVVRjdGVwMGNfVG9rZW46TWM2dWJ6eGhrbzZmTVV4bWtjOWMxVmV5bnhoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### 独立看门狗配置流程

暂时无法在飞书文档外展示此内容

## 窗口看门狗 windows WatchDog

1. 看门狗控制寄存器有七位，其中六位为递减计数器，最高位 T6 作为溢出标志位。
2. 当 T6 位为 1 时表示计数器没有溢出，反之表示溢出。
3. 若把七位寄存器看作整体，计数器在 0x40 之后溢出；若把最高位看作标志位，六位计数器在 0x00 之后溢出。
4. 窗口看门狗通过比较计数值与窗口值来判断喂狗时机，喂狗太早（计数器数值超过窗口值）、太晚（计数器减到 0）或喂狗太频繁（狗的余粮充足时喂狗）都会导致复位。

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTM5MWI5OTg5NTNlM2VmZDQ2ZWNlZjZiOGZiNmRjNzFfZjlONUVwM1YxdjBJdWFvNUI1NUhRR2hJeFBVVUFrRDlfVG9rZW46T2lJeWJ5M1Q5b2lKd0l4UDVpZGMySVE3bkRoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### WWDG工作特性

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MmU3OWQ5NzY3ZTdiMjI2ZmE5NWFkODkwZTMyOGNjM2JfWFVma0RUYlhlelRCaDAxdTBkd3pUbDdrc2RjM09UR3lfVG9rZW46T3d2amJMcG5Sb21SaVR4bUZqVGNsbkxobkhkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### WWDG超时时间

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OWZkNjI1NTU4MTBmOGNmZGFjNmNhMzYxMzQ1NzQ3MWVfWXJ0SHdyaVlxR0pOVnRxbEZLU0dGZ1lNQUREY3d4WW1fVG9rZW46R0ZhTGJQN3ozb0lObm54NDdqVmNweXY1bnNoXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# FLASH闪存

## Flash简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODg3ZTU5ZDQzNGE4MDgyZTZiMmIzY2I5YzBmYTM2YTFfMU1SQ3FtOTBhNFdDTmdscktoRE02a2d4R2d1Y1hFRmlfVG9rZW46QlltUWJpbERlbzZnRDR4REg3Z2NxdVhvbnRMXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

# OLED

驱动芯片的作用就是扫描刷新，让这个屏幕，始终都呈现出内容

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OGY1NzQ5OTZjMDg3ZDgwZWEyNDg0MjRhOWExNTYyMmFfaHhwUDJ0R082aEt6QnZUNVpnSGtxZU44ckpBMGZoUzdfVG9rZW46Um40emJCb3p2b1Z2VmN4bzh1NWNXOEpUbnY5XzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## SSD1306简介

SSD1306是一款OLED/PLED点阵显示屏的控制器，可以嵌入在屏幕中，用于

执行接收数据、显示存储、扫描刷新等任务

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGMxOTlmYjdlNTRhZDhhMDEzNDg5ZmFjMGIyYWUyZTBfNnVCVEp1cFlha0ZkM0hkQ09iU0VWNnF6WnhOdFZmc0FfVG9rZW46UnhZSGJDUG9Ub0RadUN4UHBMSGNuS0Z0bkU4XzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

### SSD1306框图以及引脚定义

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjE3OWJmY2UxOTQ5ZjU3MGE0ZTY0NDBiM2IwYzcyMTFfU2JtUEEyNHd6WG9SeGRMRjRIUmxNSFlISDdubGVzY2RfVG9rZW46TmhQamI3QUR6b1YwbFd4eXk5SGM3RDNSbjVkXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)

## 命令表

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzA2ZjhmZDE3MjIzYTk2MDUwZjI3OGFhMWRiMTdjNjlfSmJYQzlvaGszOURKYkxNNTBFR0FrME1DQXNLek0ybWRfVG9rZW46SjM5UGJpdXdQb0ZoUmh4TlJnd2N3dXdubkRjXzE3NDE0MzI4OTU6MTc0MTQzNjQ5NV9WNA)