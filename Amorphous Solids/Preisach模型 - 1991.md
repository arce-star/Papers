磁致伸缩现象的本质在于应变与磁化强度的依赖关系  

> 特别是 Terfenol 型材料具有巨大磁致伸缩效应  

但是磁致伸缩材料存在磁滞现象，给精细定位应用带来了挑战。  
如果可以预测磁滞现象就可以设计驱动器控制器来校正这些效应。  
所以引入本文要提到的 - 磁致伸缩磁滞的数学模型。  

介绍了今年来比较经典的 Preisach 模型，这个模型可以模拟磁化强度随磁场变化而产生的磁滞行为。但是磁致伸缩材料的磁滞行为与**磁场和应力**两个变量的变化密切相关。  
引出构建具有两个输入变量的 Preisach 模型的问题。  

首先考虑一种磁滞非线性模型「hysteresis nonlinearity」，模型可以用两个输入 $u(t)$ 和 $v(t)$ 以及一个输出 $f(t)$ 来表征。  
在磁致伸缩应用中， $u(t)$ 是磁场「magnetic field」，$v(t)$ 是应力「stress」，$f(t)$ 是应变「strain」。

$$
\begin{align*}
f(t) &= \int_{\alpha \ge \beta} \int  \mu(\alpha, \beta, v(t))  \hat{\gamma}_{a \beta} u(t) d\alpha  d\beta \\
&+ \int_{\alpha \ge \beta} \int  \nu(\alpha, \beta, u(t))  \hat{\gamma}_{a \beta} v(t) d\alpha  d\beta. \tag*{(1)}
\end{align*}
$$  

上述模型中 $\mu$ 依赖于 $v(t)$，$\nu$ 依赖于 $u(t)$，反映了两个输入的交叉耦合。

模型(1)由于可以等价表示为具有移动支撑「moving supports」的 $\mu(\alpha,\beta,v(t))$ 和 $\nu(\alpha,\beta,u(t))$ 模型而大大简化。  
为了得到这种表示，引入集合 $R_{u(t)}$ 和 $R_{v(t)}$ ，定义为  
$(\alpha, \beta) \in R_{u(t)}$ if $\beta_0 \le \beta \le u(t) \le \alpha \le \alpha_0$，  
$(\alpha, \beta) \in R_{v(t)}$ if $\beta_0 \le \beta \le v(t) \le \alpha \le \alpha_0
$  

考虑负饱和状态「negative saturation」然后输入单调增加「monotonic increase」直到 $u(t)$ 和 $v(t)$ 达到某些值。  
令 $f^+_{u(t)v(t)}$ 作为由此产生的输出值「resulting output value」。  
同理从正饱和「positive saturation」开始可以定义 $f^-_{u(t)v(t)}$ 。  

变换模型(1)可以得到
$$
\begin{align*}
f(t) &= \int_{R_{u(t)}} \int  \mu(\alpha, \beta, v(t))  \hat{\gamma}_{a \beta} u(t) d\alpha  d\beta \\
&+ \int_{R_{v(t)}} \int  \nu(\alpha, \beta, u(t))  \hat{\gamma}_{a \beta} v(t) d\alpha  d\beta \\
&+ \frac{1}{2}(f^+_{u(t)v(t)}+f^-_{u(t)v(t)}).
\tag*{(2)}
\end{align*}
$$  

模型(2)有两个特征属性:  
1.消去特性「Wiping-out property」  
模型(2)仅存储 $u(t)$ 和 $v(t)$ 过去主导极值的交替序列，而所有其他过去的极值均被消去。  
2.等长竖线特性「Property of equal vertical chords」  
『疑问 - 什么是次级滞后环? 这里的相等竖线指的是什么?』  
对于相同的固定 $v$ 值，所有对应于相同连续 $u(t)$ 极值的次级滞后环「minor hysteretic loops」都具有相等的竖线，无论 $u(t)$ 和 $v(t)$ 过去的变化历史如何。  
对于任何固定的 $u$ 值，由 $v(t)$ 往复变化形成的次级滞后环也同样如此。  

模型(2)还有以下独特性质:  
路径无关性「Path independence property」  
考虑 $u$-$v$ 平面上的两点 $(u_1, v_1)$ 和 $(u_2, v_2)$ 以及连接两点的一组路径，这些路径分别对应于 $u(t)$ 和 $v(t)$ 的单调变化(fig1)。那么模型(2)预测的输出增量不依赖于两点之间的特定单调路径。  
![1762418896922](image/Preisach模型-1991/1762418896922.png)  

接下来讨论模型(2)的辨识问题「identification problem」  
为了确定函数 $\mu(\alpha,\beta,v)$ 和 $\nu(\alpha,\beta,u)$，本文将使用一阶转换曲线「first-order transition curves」$f_{\alpha \beta v}$ 和 $f_{u \alpha \beta}$。  
『疑问 - 完全没看懂?』  
$f_{\alpha \beta v}$ 是两个输入分别单调增加到值 $\alpha$ 和 $v$，然后 $u(t)$ 单调减少到值 $\beta$ 时的输出。  
定义了 $F(\alpha,\beta,v)$ 和 $G(\alpha,\beta,u)$  
$$
\mu(\alpha, \beta, v) = \frac{\partial^2 F(\alpha, \beta, v)}{\partial \alpha  \partial \beta},
$$
$$
v(\alpha, \beta, u) = \frac{\partial^2 G(\alpha, \beta, u)}{\partial \alpha  \partial \beta}.
$$
在数值实现模型(2)时无需上面两个公式，只需要 $F(\alpha,\beta,v)$ 和 $G(\alpha,\beta,u)$ 的显式表达式即可完成积分。

![1762419745431](image/Preisach模型-1991/1762419745431.png)  

![1762419757383](image/Preisach模型-1991/1762419757383.png)  
对 $S^+(t)$ 积分相当于对 $R_{k}$ 积分再对 $k$ 求和

最后得到一个 $f(t)$ 的表达式，根据(3)式确定的实验测量函数 $F$ 和 $G$ 给出的输出的最终表达式。  

![1762420117694](image/Preisach模型-1991/1762420117694.png)  
应变滞后有偶对称性，其主滞后回线随磁场的变化呈现蝴蝶状。而且一级相变曲线 $f_{\alpha\beta v}$也呈现偶对称性。

『后面的讨论完全看不懂了』



