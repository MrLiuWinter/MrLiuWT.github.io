---
title: 软阈值公式
tags:
  - 图像科学
categories:
  - 数学基础
abbrlink: 51287
katex: true
math: true
date: 2020-10-25 08:50:01
---

# 软阈值公式

数学公式编辑：(转载）https://www.jianshu.com/p/4460692eece4

软阈值函数是指Y=X-T,X≥TX+T,X≤-T0,|X|[小波变换](https://baike.baidu.com/item/小波变换/10334289)的系数,T是预先选定的[阈值](https://baike.baidu.com/item/阈值/7442398)。而阈值的量化采用固定阈值法，其定义为:T=σ2log(N)，这里N为[信号采样](https://baike.baidu.com/item/信号采样/5408307)的数目，σ为噪声的标准偏差。(百度百科)

## 1、软阈值(Soft Thresholding)函数的符号

以下是各个文献中的软阈值定义符号：

​		文献【1】公式（12）：
$$
\eta_s(w,\lambda)=sgn(w)(|w|-\lambda)_+
$$
​		文献【2】：
$$
\eta_t(y)=sgn(y)(|y|-t)_+
$$
​		文献【3】：
$$
(S_\alpha(w))_k=sgn(w_k)[|w_k|-\alpha_k]_+
$$
​		文献【4】公式（8）：
$$
\widehat{x_i}=soft(z_i,\lambda w_i)=sign(z_i)max{0,|z_i|-\lambda w_i}
$$
​		文献【5】公式（1.5）：
$$
\tau_\alpha(x)_i=(|x_i|-\alpha)_+sgn(x_i)
$$
​		文献【6】公式（12）注释：
$$
soft(u,a)\equiv sign(u)max\{|u|-a,0\}
$$
​		文献【7】：
$$
soft(x, T)=\begin{cases} x+T，x\leq -T\\0 ，|x|\leq T \\x-T, x\geq T \end{cases}
$$
其中文献【1】【2】【3】【5】是第一种，也是最常见的一种；文献【4】【6】是第二种，个人认为可读性比第一种要好；文献【7】是第三种，个人认为可读性最好。当然，它们表达的意思是一样的（**无论是sgn(x)还是sign(x)都是符号函数，即当x>0时为1，当x<0时为-1**）：

​    以文献【1】符号为例解释第一种表示方式。这里w是变量，λ是阈值(非负值)，符号(|w|-λ)+表示当(|w|-λ)>0时则等于|w|-λ，当(|w|-λ)<0时则等于0。那么分三种情况来讨论：第一种情况是w>λ>0，则sgn(w)=1，|w|=w，(|w|-λ)一定大于0，(|w|-λ)+=|w|-λ，所以ηS(w,λ)=w-λ；第二种情况是w<-λ<0，则sgn(w)=-1，|w|=-w，(|w|-λ)也一定大于0，(|w|-λ)+=|w|-λ，所以ηS(w,λ)=-1*(-w-λ)= w+λ；第三种情况是|w|<λ，此时(|w|-λ)一定小于0，则(|w|-λ)+=0，所以ηS(w,λ)=0。因此

![img](http://img.blog.csdn.net/20160809165935019)

 

​    以文献【6】符号为例解释第二种表示方式。这种表示方式中符号max{|u|-a,0}的作用与第一种表示方式中的符号(|w|-λ)+的作用一样，即当(|u|-a)>0时max{|u|-a,0}=(|u|-a)，当(|u|-a)<0时max{|u|-a,0}=0，知道了这一点剩下的分析与第一种表示方式相同。

​    综上，三种表示方式均是一致的。

# 2、软阈值(Soft Thresholding)函数的作用

​    弄清楚了软阈值(Soft Thresholding)的符号表示以后，接下来说一说它的作用。以下内容主要参考了文献【7】，这是一个非常棒的PPT！！！

​    软阈值(SoftThresholding)可以求解如下优化问题：

![img](http://img.blog.csdn.net/20160803142929994)

 

其中：

![img](http://img.blog.csdn.net/20160803143000495)

​    根据范数的定义，可以将上面优化问题的目标函数拆开：

![img](http://img.blog.csdn.net/20160803143016510)

​    也就是说，我们可以通过求解N个独立的形如函数

![img](http://img.blog.csdn.net/20160803143028042)

的优化问题，来求解这个问题。由中学时代学过的求极值方法知道，可以求函数*f*(*x*)导数：

![img](http://img.blog.csdn.net/20160803143048448)

​    这里要解释一下变量x绝对值的导数，当x>0时，|x|=x，因此其导数等于1；当x<0时，|x|=-x，因此其导数等于-1；综合起来，x绝对值的导数等于sgn(x)。令函数*f*(*x*)导数等于0，得：

![img](http://img.blog.csdn.net/20160803143100948)

​    这个结果等号两端都有变量x，需要再化简一下。下面分三种情况讨论：

(1)当b>λ/2时

​    假设x<0，则sgn(x)=-1，所以x=b+λ/2>0，与假设x<0矛盾；

​    假设x>0，则sgn(x)=1，所以x=b-λ/2>0，成立；

​    所以此时在x=b-λ/2>0处取得极小值：

![img](http://img.blog.csdn.net/20160803143124933)

 

​    即此时极小值小于*f*(0)，而当x<0时

![img](http://img.blog.csdn.net/20160803143205402)

​    即当x<0时函数*f*(*x*)为单调降函数（对任意△*x*<0，*f*(0)<*f*(△*x*)）。因此，函数在x=b-λ/2>0处取得最小值。

(2)当b<-λ/2时

​    假设x<0，则sgn(x)=-1，所以x=b+λ/2<0，成立；

​    假设x>0，则sgn(x)=1，所以x=b-λ/2<0，与假设x<0矛盾；

​    所以此时在x=b+λ/2<0处取得极小值：

![img](http://img.blog.csdn.net/20160803143230652)

​    即此时极小值小于*f*(0)，而当x>0时

![img](http://img.blog.csdn.net/20160803143241212)

​    即当x>0时函数*f*(*x*)为单调升函数（对任意△*x*>0，*f*(△*x*)>*f*(0)）。因此，函数在x=b+λ/2<0处取得最小值。

(3)当-λ/2<b<λ/2时(即|b|<λ/2时)

​    假设x<0，则sgn(x)=-1，所以x=b+λ/2>0，与假设x<0矛盾；

​    假设x>0，则sgn(x)=1，所以x=b-λ/2<0，与假设x<0矛盾；

​    即无论x为大于0还是小于0均没有极值点，那么x=0是否为函数*f*(*x*)的极值点呢？

​    对于△*x*≠0，

![img](http://img.blog.csdn.net/20160803143323199)

​    当△*x* >0时，利用条件b<λ/2可得

![img](http://img.blog.csdn.net/20160803143336198)

​    当△*x* <0时，利用条件b<λ/2可得(注：此时|△*x* |=-△*x*)

![img](http://img.blog.csdn.net/20160803143355746)

​    因此，函数在x=0处取得极小值，也是最小值。

​    综合以上三种情况，*f*(*x*)的最小值在以下位置取得：

![img](http://img.blog.csdn.net/20160803143406042)

​    与前面的软阈值(Soft Thresholding)对比一下，发现了么？若将上式中的b视为变量，λ/2视为阈值，上式即为软阈值(SoftThresholding)的公式。

​    至此，我们可以得到优化问题

![img](http://img.blog.csdn.net/20160803142929994)

的解为

![img](http://img.blog.csdn.net/20160803143439637)

​    注：该式为软阈值(Soft Thresholding)的矩阵形式。

# 3、软阈值(Soft Thresholding)的变形

​    当优化问题变为

![img](http://img.blog.csdn.net/20160803143452950)

​    因为对目标函数乘一个常系数不影响极值点的获得，所以可等价为优化问题

![img](http://img.blog.csdn.net/20160803143508356)

此时的解为*soft*(*B*, *λ*)。

# 4、软阈值(Soft Thresholding)的MATLAB代码

​    软阈值(Soft Thresholding)的函数代码可以写成专门针对优化问题

![img](http://img.blog.csdn.net/20160803142929994)

​    软阈值(Soft Thresholding)是如此简单以至于可以用一句代码去实现它[8]：

　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　![img](https://images2018.cnblogs.com/blog/389051/201712/389051-20171203171206351-1917148791.png)

 当然，如果不习惯这种形式，也可以写成常见的函数形式：

```
function` `[ soft_thresh ] = softthresholding( b,lambda ) ``  ``soft_thresh = ``sign``(b).*``max``(``abs``(b) - lambda/2,0); ``end
```

　　

​    一定要注意：这种写法是针对最开始的优化问题：

![img](http://img.blog.csdn.net/20160803142929994)

​    但我个人感觉更应该写成这种通用形式：

```
function` `[ x ] = soft( b,T ) ``  ``x = ``sign``(b).*``max``(``abs``(b) - T,0); ``end
```

　　

​    如此之后，若要解决优化问题

![img](http://img.blog.csdn.net/20160803142929994)

只需调用soft(B, λ/2)即可；若要解决优化问题

![img](http://img.blog.csdn.net/20160803143452950)

只需调用soft(B, λ)即可。

# 5、软阈值(Soft Thresholding)测试代码

​    用以下一小段代码测试一下软阈值，用来求解优化问题：

![img](http://img.blog.csdn.net/20160803145313085)

这里用的对比函数是基追踪降噪(BPDN_quadprog.m)，参见压缩感知重构算法之基追踪降噪(Basis PursuitDe-Noising, BPDN)（http://blog.csdn.net/jbb0523/article/details/52013669），使用BPDN时，实际上就是观测矩阵为单位阵时的一种特殊情况：

```
clear` `all``;``close` `all``;``clc``; ``b = [-0.8487  -0.3349  0.5528  1.0391  -1.1176]'; ``lambda = 1; ``x1=soft(b,lambda) ``x2=BPDN_quadprog(b,``eye``(``length``(b)),lambda) ``fprintf``(``'\nError between soft and BPDN = %f\n'``,``norm``(x1-x2)) 
```

　　

这里就不给出输出结果了。运行后，观察输出结果可知，soft函数与BPDN_quadprog函数的输结果相同。

​    另外，可以在matlab里输入以下命令看一个软阈值的图像：

```
x=-5:0.1:5;T=1;y=soft(x,T);``plot``(x,y);``grid``; 
```

　　

![img](http://img.blog.csdn.net/20160803143835830)

 

# 6、总结

 

​    可以发现，软阈值解决的优化问题和基追踪降噪问题很像，但并不一样，而且需要格外说明的是，软阈值并能不解决基追踪降噪问题，文献【8】在最后明确说明了这一点：

![img](http://img.blog.csdn.net/20160803143913753)

 

​    近来学习研究各种算法，发现给自己挖的坑有点深，有点跳不出来了，各种问题接踵而来，各种新概念一个接着一个，而软阈值(Soft Thresholding)就是其中之一，根本没法子绕过去。在文献【6】中，作者描述软阈值(Soft Thresholding)时用的是“the well-known soft-threshold function”，好吧，还well-kown。在学习过程中文献【9】对我帮助也挺大的，但从作者的语气来看，也没有多么well-kown啊……

​    最后，非常感谢文献【7】的PPT，看了之后让我有一种醍醐灌顶的感觉……

# 7、参考文献

【1】Donoho D L, JohnstoneJ M. Ideal spatial adaptation by wavelet shrinkage[J]. Biometrika, 1994, 81(3):425-455.

【2】Donoho D L.De-noising by soft-thresholding[J]. IEEE transactions on information theory,1995, 41(3): 613-627.

【3】Bredies K, Lorenz D.Iterative soft-thresholding converges linearly[R]. Zentrum fürTechnomathematik, 2007.

【4】Bioucas-Dias J M,Figueiredo M A T. A new TwIST: two-step iterative shrinkage/thresholdingalgorithms for image restoration[J]. IEEE Transactions on Image processing,2007, 16(12): 2992-3004.

【5】Beck A, Teboulle M. Afast iterative shrinkage-thresholding algorithm for linear inverse problems[J].SIAM journal on imaging sciences, 2009, 2(1): 183-202.

【6】Wright S J, Nowak RD, Figueiredo M A T. Sparse reconstruction by separable approximation[J]. IEEETransactions on Signal Processing, 2009, 57(7): 2479-2493.

【7】谷鹄翔.IteratedSoft-Thresholding Algorithm[Report,slides]. http://www.sigvc.org/bbs/thread-41-1-2.html

【8】http://www.simonlucey.com/soft-thresholding/

【9】http://blog.sina.com.cn/s/blog_6d0e97bb01015vq3.html