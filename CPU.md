# CPU

> Powered by YDJSIR
>
> 下面的分类可能不是很严谨，只是把知识对照起来看

## 运算器

> 只涉及课程中提到的内容

### ALU

> - Lecture04
>
> - Lecture05
>
> 考虑到这部分内容通常已经在机考中涉及，这里不作重点但仍会提及。

#### 1. 移位运算

##### 1.算数移位：

+ **符号位不变**, 左移相当于乘以 2, 右移相当于除以 2(左侧全补符号位).

##### 2. 逻辑移位:

+ **无符号数的移位**, 右移时永远在高位填 0.

##### 3. 循环移位

- 和它的名字一样

#### 2. 加法运算

##### 1. 全加器

   + $𝑆_𝑖=𝑋_𝑖⊕𝑌_𝑖⊕𝐶_{𝑖−1}$
   + $𝐶_𝑖=𝑋_𝑖𝐶_{𝑖−1}+𝑌_𝑖𝐶_{𝑖−1}+𝑋_𝑖𝑌_𝑖$

##### 2. Serial Carry Adder

   <iframe frameborder="0" style="width:150%;height:200%;" src="https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1#R7VpLc9owEP41HJvxS9g%2BJpC0h3amMxxKjipWsDrGYmwRIL%2B%2BMpZfWiAE%2FMAMF8ZaybL0fatvd20G5mix%2BR7hpf%2BLeSQYGJq3GZjjgWG4riF%2BE8M2NdjITA3ziHqpSS8ME%2FpBpFGT1hX1SFwZyBkLOF1WjTMWhmTGKzYcRWxdHfbGgupTl3hOgGEywwG0%2FqEe91OrY9iF%2FQehcz97sj50054FzgbLncQ%2B9ti6ZDKfB%2BYoYoynV4vNiAQJdhku6X0vB3rzhUUk5KfcYMslx3ybbY54Yq%2ByySLuszkLcfBcWJ8itgo9ksygiVYx5idjS2HUhfEf4XwricMrzoTJ54tA9pIN5VN5e3L9mlw%2FINkab0pd461spOtMFndwq9IUs1U0k6NsPQdVOCNhC8KjrRgTkQBz%2Bl6dC0u3mOfj8lt%2FMyqeYmjSgy1T8icdWM%2Fa2RQcR3PC5V0F%2FuKitIzCtGNlP0Ou3gVDV4U2UtA2GgPblmt7x8FKrvblEeC%2F9iknkyXebXstFK6KHY6Xqei80U3CgQTznUScbI7DCaHLHM6tQpA11yX5kSa%2FpDyOdhjrCkzHMDEAJtAjQ%2B8x0VXRmgU4julMOfCheOi03Cgd%2BaRZnPld6%2BuHPvWB425YAgvtASuzXeitw%2BEn2pCeGOCu0O3VifTm%2FN4EHI80wLJwX664ekDnYUK6oINEwpA4ORWB8lF2LKjnpYpEYvqB%2F%2B6mSphdJqve7QM9DdA4mUuIUJzqkV7PoRlqCoCaDU6NuccRVH0569S4PZJttOcMDS%2BU8lOBcrrJQNoVJNRMFqKfl4WAiUz7PMkSmo%2B3pWHyUF%2BoRehKY7BhdRaDHbNHanKpchxw9tYy7nQDV%2BiAutadA2owQYCFSd8SBAt1lyA4FkQ07D2iQ6c7QB0AKBTNok4JWZiA5OHY32mkfp72dVVlmE5NVUaLrzIc90sMHa8ktQcjT9Zey503VEoiJcHLg%2BCXS0k1etqNkezCSHF9JHdGKKqLUDVyNUioAQid9D%2F0q%2B8UEcylmgpULnzZMu0%2FoJaL9rt2G4jCXOq1%2F4gis0NEERTt6yk4ay8uDSWbOvELw6fzuKfJ%2BzmqDIvUe5jNaRjWFGbViZoMs%2Fad0MPVjlYToepETRIK69FJ%2BK3%2FYcmwrQqEezInq6moBAvI6U1Aah1w7xYwzV8qlpOnmwBVjemtgnrV%2F9qoPX%2FSVQc%2BM39S52kuf9I1WNbe423Og1FTvFUnajDe6hqsq%2B%2BM5kTUlRKrEzXKKKzrJ%2F3%2FRqKKXIuvnnQNflyf3gCih8qDViCFlfjrDUB6QkpaE6SiWfzhOZWJ4l%2Fj5vN%2F"></iframe>

+ 缺点: 速度慢.
+ 延时(OR AND 1ty, XOR 3ty)
  + Cn: 2n ty
  + Sn: 2n+1 ty

##### 3. Carry Look Ahead Adder

**注意**：这里的+均为“或”
$$
\begin{aligned}
𝐶_𝑖&=𝑋_𝑖𝐶_{𝑖−1}+𝑌_𝑖𝐶_{𝑖−1}+𝑋_𝑖𝑌_i\\
\\
C_1&=𝑋_1𝑌_1+(𝑋_1+𝑌_1)𝐶_0\\
𝐶_2&=𝑋_2𝑌_2+(𝑋_2+𝑌_2)𝑋_1𝑌_1+(𝑋_2+𝑌_2)(𝑋_1+𝑌_1)𝐶_0\\
𝐶_3&=𝑋_3𝑌_3+𝑋_3+𝑌_3𝑋_2𝑌_2+𝑋_3+𝑌_3𝑋_2+𝑌_2𝑋_1𝑌_1
+(𝑋_3+𝑌_3)(𝑋_2+𝑌_2)(𝑋_1+𝑌_1)𝐶_0\\
C_4 &=...
\end{aligned}
$$

可见,$Ci$ 仅与最初的X Y和 $C_0$有关.
令$𝑃_𝑖=𝑋_𝑖+𝑌_𝑖, 𝐺_𝑖=𝑋_𝑖𝑌_i$
则:
$$
\begin{aligned}
\\
𝐶_1&=𝐺_1+𝑃_1𝐶_0\\
𝐶_2&=𝐺_2+𝑃_2𝐺_1+𝑃_2𝑃_1𝐶_0\\
𝐶_3&=𝐺_3+𝑃_3𝐺_2+𝑃_3𝑃_2𝐺_1+𝑃_3𝑃_2𝑃_1𝐶_0\\
𝐶_4&=...
\end{aligned}
$$
总结得:$C_{i+1} = G_{i+1}+P_{i+1}C_i$, 超前进位加法器采用的是将低一位的逻辑代数代入高一位, 依此类推最终每一个进位输出仅考虑 $C_0, X_i, Y_i$几个信号, 于是所有的进位都能同时计算.

+   缺点:复杂
+   延时: 1 ty+ 2ty + 3 ty = 6 ty

#### 4. Partial Carry Look Ahead Adder

   结合两者，比如说4个8位的Carry Look Ahead Adder组合成一个32位的加法器。

#### 5. 溢出判断

+ $C_n\oplus C_{n-1} =1$, 即符号位进位与最高有效位进位不同时,发生溢出.
+ $𝑋_𝑛 𝑌_𝑛 \overline{𝑆_𝑛}+\overline{𝑋_𝑛𝑌_𝑛}𝑆_𝑛=1$,则溢出,与上面等价.

#### 3. 减法运算

减法运算大致与加法相同,只需要将减数`取反加一`然后按加法算即可, **注意加一的操作是令 $C_0 = 1$**。

#### 4. 乘法运算

##### 1. 无符号整数乘法

通过**加法和移位实现**,与竖式乘法极其类似,但是计算机很难像人类那样一次性把各位乘的结果一次性相加,因此采用部分积的方式:
例:$0111\times0110$

| <font color=#FF0000>部分积</font> |              乘数               |       得到当前行的操作       |
| :-------------------------------: | :-----------------------------: | :--------------------------: |
|  <font color=#FF0000>0000</font>  |              0110               | 部分积+乘数末位$\times 0111$ |
|  <font color=#FF0000>0000</font>  | <font color=#FF0000>0</font>011 |             右移             |
|  <font color=#FF0000>0111</font>  | <font color=#FF0000>0</font>011 | 部分积+乘数末位$\times 0111$ |
|  <font color=#FF0000>0011</font>  | <font color=#FF0000>10</font>01 |             右移             |
|  <font color=#FF0000>1010</font>  | <font color=#FF0000>10</font>01 | 部分积+乘数末位$\times 0111$ |
|  <font color=#FF0000>0101</font>  | <font color=#FF0000>010</font>0 |             右移             |
|  <font color=#FF0000>0101</font>  | <font color=#FF0000>010</font>0 | 部分积+乘数末位$\times 0111$ |
|  <font color=#FF0000>0010</font>  | <font color=#FF0000>1010</font> |             右移             |

+ 乘数末位决定被乘数是否加到部分积,然后部分积和乘数均**右移**,部分积低位保存到乘数高位.
+ **被乘数只与部分积高位相加**

原理:
$$\begin{aligned}
XY &= XY_nY_{n-1}...Y_2Y_1\\&=X(Y_n\times2^{n-1}+Y_n\times2^{n-2}+...+Y_2\times2^1+Y_1\times2^0)\\&=2^n(XY_n\times2^{-1}+XY_{n-1}\times2^{-2}+...+XY_1\times2^{-n})\\
&=2^nP_{n},其中P_{n} = 2^{-1}\times(XY_{n}+P_{n-1}),n\gt1.\end{aligned}$$

##### 2. 补码整数乘法

根据上面无符号整数的原理, 可以将二进制补码整数相乘变形如下:

$$\begin{aligned}XY& = XY_nY_{n-1}...Y_2Y_1\\&=X(-Y_n\times2^{n-1}+Y_n\times2^{n-2}+...+Y_2\times2^1+Y_1\times2^0)\\&=2^nX((Y_{n-1}-Y_n)\times2^{-1}+(Y_{n-2}-Y_{n-1})\times2^{-2}+...+(Y_0-Y_1)\times2^{-n})\\&
=2^nP_{n},其中Y_0=0,P_{n} = 2^{-1}\times(X(Y_{n-1}-Y_{n})+P_{n-1}),n\gt1.\end{aligned}$$

形式上还原了,只是每次乘的**不是乘数的末位数**, 且注意是**算数右移**,需要补符号位,
例: $-7\times-6 = 42,即 1001\times1010=00101010$

| <font color=#FF0000>部分积</font> |               乘数               |       得到当前行的操作        |
| :-------------------------------: | :------------------------------: | :---------------------------: |
|  <font color=#FF0000>0000</font>  | 1010<font color=#0000FF>0</font> | 部分积+$(Y_0-Y_1)\times 1001$ |
|  <font color=#FF0000>0000</font>  | <font color=#FF0000>0</font>1010 |             右移              |
|  <font color=#FF0000>0111</font>  | <font color=#FF0000>0</font>1010 | 部分积+$(Y_1-Y_2)\times 1001$ |
|  <font color=#FF0000>0011</font>  | <font color=#FF0000>10</font>101 |             右移              |
|  <font color=#FF0000>1100</font>  | <font color=#FF0000>10</font>101 | 部分积+$(Y_2-Y_3)\times 1001$ |
|  <font color=#FF0000>1110</font>  | <font color=#FF0000>010</font>10 |             右移              |
|  <font color=#FF0000>0101</font>  | <font color=#FF0000>010</font>10 | 部分积+$(Y_3-Y_4)\times 1001$ |
|  <font color=#FF0000>0010</font>  | <font color=#FF0000>1010</font>1 |             右移              |

#### 5. 除法运算

##### 1. unsigned

1.人的计算:除数右移, 2n位

+ 竖式计算:
  <img src="https://i0.hdslb.com/bfs/article/8216b980b855f3139a28932f6883a053a6e04f1f.png" style="zoom:50%;" />

|   余数   |   <font color=#0000FF>除数</font>   |               商                |
| :------: | :---------------------------------: | :-----------------------------: |
| 00000111 | <font color=#0000FF>00110000</font> |              0000               |
| 00000111 | 0<font color=#0000FF>0011000</font> |              0000               |
| 00000111 | 0<font color=#0000FF>0011000</font> | 000<font color=#FF0000>0</font> |
| 00000111 | 00<font color=#0000FF>001100</font> | 000<font color=#FF0000>0</font> |
| 00000111 | 00<font color=#0000FF>001100</font> | 00<font color=#FF0000>00</font> |
| 00000111 | 000<font color=#0000FF>00110</font> | 00<font color=#FF0000>00</font> |
| 00000001 | 000<font color=#0000FF>00110</font> | 0<font color=#FF0000>001</font> |
| 00000001 | 0000<font color=#0000FF>0011</font> | 0<font color=#FF0000>001</font> |
| 00000001 | 0000<font color=#0000FF>0011</font> | <font color=#FF0000>0010</font> |





2. 计算机的计算: **余数左移**, n位

| <font color=#0000FF>余数</font> |               <font color=#FF0000>商</font>                | 除数 |
| :-----------------------------: | :--------------------------------------------------------: | :--: |
| <font color=#0000FF>0000</font> |              <font color=#0000FF>0111</font>               | 0011 |
| <font color=#0000FF>0000</font> |               <font color=#0000FF>111</font>               | 0011 |
| <font color=#0000FF>0000</font> | <font color=#0000FF>111</font><font color=#FF0000>0</font> | 0011 |
| <font color=#0000FF>0001</font> | <font color=#0000FF>11</font><font color=#FF0000>0</font>  | 0011 |
| <font color=#0000FF>0001</font> | <font color=#0000FF>11</font><font color=#FF0000>00</font> | 0011 |
| <font color=#0000FF>0011</font> | <font color=#0000FF>1</font><font color=#FF0000>00</font>  | 0011 |
| <font color=#0000FF>0000</font> | <font color=#0000FF>1</font><font color=#FF0000>001</font> | 0011 |
| <font color=#0000FF>0001</font> |               <font color=#FF0000>001</font>               | 0011 |
| <font color=#0000FF>0001</font> |              <font color=#FF0000>0010</font>               | 0011 |

##### 2. 带有符号的除法

+ 如何判断余数(的绝对值)是否大于除数(的绝对值)?
  + 同号则减, 异号则加. 与结果符号相同的那个数绝对值大

<table style="border-collapse:collapse;margin-left:52.305pt" cellspacing="0"><tbody><tr style="height:29pt"><td style="width:94pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt" rowspan="2"><p class="s116" style="padding-top: 2pt;padding-left: 6pt;padding-right: 5pt;text-indent: 0pt;line-height: 22pt;text-align: center;">remainder</p><p class="s116" style="padding-left: 6pt;padding-right: 5pt;text-indent: 0pt;line-height: 22pt;text-align: center;">sign</p></td><td style="width:74pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt" rowspan="2"><p class="s116" style="padding-top: 2pt;padding-left: 10pt;padding-right: 9pt;text-indent: 0pt;line-height: 22pt;text-align: center;">Divisor</p><p class="s116" style="padding-left: 10pt;padding-right: 9pt;text-indent: 0pt;line-height: 22pt;text-align: center;">sign</p></td><td style="width:211pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt" colspan="2"><p class="s116" style="padding-top: 2pt;padding-left: 62pt;text-indent: 0pt;text-align: left;">Subtraction</p></td><td style="width:216pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt" colspan="2"><p class="s116" style="padding-top: 2pt;padding-left: 74pt;padding-right: 73pt;text-indent: 0pt;text-align: center;">Addition</p></td></tr><tr style="height:29pt"><td style="width:106pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s116" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">0</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s116" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">1</p></td><td style="width:111pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s116" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">0</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s116" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">1</p></td></tr><tr style="height:29pt"><td style="width:94pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">0</p></td><td style="width:74pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">0</p></td><td style="width:106pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">Enough</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">Not enough</p></td><td style="width:111pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 11pt;padding-right: 10pt;text-indent: 0pt;text-align: center;">----</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">----</p></td></tr><tr style="height:29pt"><td style="width:94pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">0</p></td><td style="width:74pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">1</p></td><td style="width:106pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">----</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">----</p></td><td style="width:111pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 11pt;padding-right: 10pt;text-indent: 0pt;text-align: center;">Enough</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">Not enough</p></td></tr><tr style="height:29pt"><td style="width:94pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">1</p></td><td style="width:74pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">0</p></td><td style="width:106pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">----</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">----</p></td><td style="width:111pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 11pt;padding-right: 10pt;text-indent: 0pt;text-align: center;">Not enough</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">Enough</p></td></tr><tr style="height:29pt"><td style="width:94pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">1</p></td><td style="width:74pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;text-indent: 0pt;text-align: center;">1</p></td><td style="width:106pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">Not enough</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">Enough</p></td><td style="width:111pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 11pt;padding-right: 10pt;text-indent: 0pt;text-align: center;">----</p></td><td style="width:105pt;border-top-style:solid;border-top-width:1pt;border-left-style:solid;border-left-width:1pt;border-bottom-style:solid;border-bottom-width:1pt;border-right-style:solid;border-right-width:1pt"><p class="s117" style="padding-top: 2pt;padding-left: 8pt;padding-right: 7pt;text-indent: 0pt;text-align: center;">----</p></td></tr></tbody></table>

<img src="https://i0.hdslb.com/bfs/article/aadda87e9086a37cb714b2970fa7596c0721f939.png" width = "30%" />

1. **恢复余数法** 在下面的步骤中,余数和除数的和是存储在余数寄存器里面的,判断完成后,还要恢复原来的余数(即减去余数).之前的不带符号位除法**也都是恢复余数法**,只是没有表示出来.

   | <font color=#0000FF>余数</font> |               <font color=#FF0000>商</font>                | 除数 |        得到本步操作        |
   | :-----------------------------: | :--------------------------------------------------------: | :--: | :------------------------: |
   | <font color=#0000FF>1111</font> |              <font color=#0000FF>1001</font>               | 0011 |             -              |
   | <font color=#0000FF>1111</font> |               <font color=#0000FF>001</font>               | 0011 |            左移            |
   | <font color=#0000FF>1111</font> | <font color=#0000FF>001</font><font color=#FF0000>0</font> | 0011 | 1111+0011 =0010,not enough |
   | <font color=#0000FF>1110</font> | <font color=#0000FF>01</font><font color=#FF0000>0</font>  | 0011 |            左移            |
   | <font color=#0000FF>1110</font> | <font color=#0000FF>01</font><font color=#FF0000>00</font> | 0011 | 1110+0011=0001, not enough |
   | <font color=#0000FF>1100</font> | <font color=#0000FF>1</font><font color=#FF0000>00</font>  | 0011 |            左移            |
   | <font color=#0000FF>1111</font> | <font color=#0000FF>1</font><font color=#FF0000>001</font> | 0011 |   1100+0011=1111, enough   |
   | <font color=#0000FF>1111</font> |               <font color=#FF0000>001</font>               | 0011 |            左移            |
   | <font color=#0000FF>1111</font> |              <font color=#FF0000>0010</font>               | 0011 | 1111+0011=0010,not enough  |

   **最后,结果取 <font color=#FF0000>0010</font> 的补码整数 <font color=#FF0000>1110 </font>为最终结果.**

   + 缺点:Problem: recover remainder is high cost
   + 解决方案:使用不恢复余数法(加减相消法)

2. 加减相消法.

   + 规则 
     + 将被除数符号拓展 n 位后存储在余数和商寄存器.
     + 如果被除数与除数符号相同, 作减法; 若符号位不同, 作加法.
       + 若新的**余数与除数符号相同, 上商 1**; 否则上商 0.
     + 新的余数(指左移前的余数)与除数符号位相同, 则 $R_{i+1}= 2R_i-Y$, 即`余数=余数<<1-除数`;否则$R_{i+1}= 2R_i+Y$
   + 商的修正:
     + **商左移一位. 若被除数和除数异号(即商为负), 商加一**
     + 若余数与被除数符号不同:
       + 若被除数和除数同号,余数加除数 
       + 若被除数和除数异号,余数减除数
     + 注意：若做完如上修正后，余数为除数相反数，需要将余数置为0，同时商减一
   + 示例:
     <img src="https://i0.hdslb.com/bfs/article/35ad64b739a0dbd5d9908dcf33a496f7bd10bac0.png" >

#### BCD 码

+ 每 4 位二进制数表示十进制的一位数

+ 加法:由于真值的进位是 10,而 BCD 码的进位是 16,所以在真值产生进位的时候需加 6 强制进位.

+ 减法:类似于补码减法. BCD"补码"与原码相加得 9.若结果是负数("补码"表示),需转化成负号+原码的形式.
  $𝑁1−𝑁2=𝑁1+(10^𝑛−𝑁2)$
  **计算补码**

  “Invert” 每一位, 并在最后一位加一(注意：这里的位指的是整个NBCD数的最后一位！)
  **“Invert” NBCD数位**

  - 反转每一位,并加上 “1010”
  - 加上“0110”, 并反转每一位



### FPU

> - Lecture06

#### 浮点数的加减运算

$X=X_S \times 2^{X_E},Y=Y_S \times 2^{Y_E}$

+ 步骤
  1. 检查是否为零
  2. 阶码对齐,尾数移位
  3. 对尾数加或减
  4. 标准化结果
  5. 溢出判断

1. 对阶

   1. 求阶差
      $\Delta E=\begin{cases}
        =0,已经对齐\\
      \ne0,\begin{cases}大的向小的对齐:减小较r大的阶码,同时扩大其尾数\\小的向大的对齐:增大较小的阶码,同时减小其尾数 \end{cases} \\
      \end{cases}$
      在计算机中,尾数左移可能会使最高位数据丢j失,故采用小阶向大阶对齐
      ![浮点数加减](https://i0.hdslb.com/bfs/article/deb6114c1afee838908c5071612f84f69a0fa8d0.jpg)

    <center>浮点数加减的过程</center>

##### 一些溢出情况

###### 1. Exponent overflow

  + 一个正的指数超出了指数的最大值(即127)
  + 指定为$-\infty 或 +\infty$

###### 2. Exponent underflow

  + 一个负的指数小于了指数的最小值(即-126)
  + 指定为0.

###### 3. Significand overflow

  + 同号的两个数字相加时,在最重要的位上产生了进位.
  + 在realignment时修正

###### 4. Significand underflow

  + 在对齐尾数的时候, 数据可能从尾数的最右端流失
  + 需要某种形式的四舍五入

##### 原码加减法(用于尾数的加减)

+ 如果两个操作数符号相同,做加法,否则做减法.

  + 加法:
    + 若最高位产生了进位,溢出
    + 符号同加数
  + 减法:加第二个数的补数
    + 若最高位产生进位,结果正确(符号等同于被减数)
    + 若没有进位,应该取结果的补数,最终结果与被减数相反.
      注意:此处可以是认定为没有符号位的补码在做计算,所以最终结果需要进行修正.(因为正数补码是它自身,负数补码是其反码加一) 
      ![浮点数运算源码加减法](https://i0.hdslb.com/bfs/article/baa713a920ac0acf967f9b22dda0cc73973d0598.png)

  更通俗的说法:最终算A+B的时候(无论是一开始就是A+B还是减法转化而来).如A,B同号,尾数是正常相加;若A,B异号,尾数为$A_S+[B_S]_补$

##### 浮点数加减法举例

+ 减法
  0.5-(-0.4375)=0.5+0.4375=0.9375
  0.5&emsp;&emsp;&emsp;<font color=RED>0</font>&emsp;<font color=BLUE>01111110</font>&emsp;<font color=GREEN>00000000000000000000000</font>
  -0.4375&emsp;<font color=RED>1</font>&emsp;<font color=BLUE>01111101</font>&emsp;<font color=GREEN>11000000000000000000000</font>
  &ensp;0.4375&emsp;<font color=RED>0</font>&emsp;<font color=BLUE>01111101</font>&emsp;<font color=GREEN>11000000000000000000000</font>
  <font color = BLUE>01111110-01111101=01111110+10000011=00000001</font>
  则前者阶码比后者大,后者向前者对齐(后者阶码加1,尾数右移一位,此处尾数包含隐藏位，即橙色位).减法经处理后,两个操作数同号,尾数做正常加法

  <center>&emsp;<font color=#FF8500>1</font>&emsp;<font color=GREEN>0000...00</font></center>
  <center>+&ensp;<font color = GREEN>0</font>&emsp;<font color=#FF8500>1</font><font color=GREEN>110...00</font></center>
  <center>——————————</center>
  <center><font color=#FF8500>&emsp;1</font>&emsp;<font color=GREEN>1110...00</font></center>

  加法计算没有进位，则结果正确，为

<center><font color=RED>1</font>&emsp;<font color=BLUE>01111101</font>&emsp;<font color=GREEN>11000000000000000000000</font></center>

+ 加法
  0.5+(-0.4375)=0.0625
  0.5&emsp;&emsp;&emsp;<font color=RED>0</font>&emsp;<font color=BLUE>01111110</font>&emsp;<font color=GREEN>00000000000000000000000</font>
  -0.4375&emsp;<font color=RED>1</font>&emsp;<font color=BLUE>01111101</font>&emsp;<font color=GREEN>11000000000000000000000</font>

  <font color = BLUE>01111110-01111101=01111110+10000011=00000001</font>
  则前者阶码比后者大,后者向前者对齐(后者阶码加1,尾数右移一位,此处尾数包含隐藏位，即橙色位).两个操作数异号,尾数加法做加后者补数.

  <center>&emsp;<font color=#FF8500>1</font>&emsp;<font color=GREEN>0000...00</font></center>
  <center>+&ensp;<font color = GREEN>1</font>&emsp;<font color=#FF8500>0</font><font color=GREEN>010...00</font></center>
  <center>——————————</center>
  <center><font color = RED>1</font><font color=#FF8500>&ensp;0</font>&emsp;<font color=GREEN>0010...00</font></center>

  符号相异产生进位,结果正确,与第一个操作数符号相同.经规格化后:

  <center><font color=RED>1</font>&emsp;<font color=BLUE>01111011</font>&emsp;<font color=GREEN>00000000000000000000000</font></center>

#### 浮点数乘法

![浮点数乘](https://i0.hdslb.com/bfs/article/16896fbb58f26550525aedbf82281f8eec4abede.jpg)

+ 步骤
  + 如果任何一个操作数为0,返回0.
  + 指数相加时需要减去偏差值,因为阶码用移码表示.
  + 尾数相乘.
  + 结果规格化并舍入.(可能造成指数溢出).

#### 浮点数除法

![浮点数除法](https://i0.hdslb.com/bfs/article/2489c91543786aa46bdfc31c6d4f6b1851450557.jpg)

+ 步骤
  + 除数为0,报错或设为无穷.
  + 被除数为0,设为0.
  + 被除数的阶码和除数的阶码做差,并加回偏差值.
  + 尾数相除.
  + 结果标准化并舍入.

**注意**:**和无符号整数除法不同**:浮点数除法给被除数后面填零存入余数和商寄存器,而整数是高位填零.

### 保护位

为了提高精度,在计算时每个数字都存在保护位,暂时储存着计算后(比如右移)后的超出低位的数据,到最后再将他们规约掉。



### Transformer

> YDJSIR不清楚这是否是一个真正的物理单元，这里仅仅是提供一个逻辑上的概念。
>
> 当然即使真的是一个真正的物理单元，他也绝不像软院特色PA那么简单。
>
> 这部分内容在HW01里面应该展现得淋漓尽致了
>
> - Lecture03





## 控制器

> - Lecture16

### ICC



### MMU



### 流水线



## IO模块

> 在`IO.md`里面展开



## 寄存器

> - Lecture15



## 指令集与指令执行过程

> - Lecture14

### 中断：

有了中断，处理器可以在进行 I/O 操作时执行其他指令。提供中断主要是为了提高效率，因为大部分外设的速度都比处理器慢得多，假如没有中断，每次 I/O 操作后处理器都会进入空闲状态直到外设跟上进度。

+ 默认开

+ 程序可以在执行指令的时候执行另一条指令

  <iframe frameborder="0" style="width:100%;height:280px;" src="https://app.diagrams.net/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1#R3VjLcpswFP0abTO8H0uwcbtoZzqTRZOlYlRQByNGyLGdr68EEkKGpHk4dpJMJiMdriR07rmPANzFZv%2BNwqb8SXJUAcfK98BdAsfxHZf%2FFcChB1wn7oGC4ryHbA1c4wckQUuiW5yj1jBkhFQMNya4JnWN1szAIKVkZ5r9IZV5agMLNAGu17Caor9xzsoejZxQ498RLkp1sh3I%2B22gMpY3aUuYk90IcjPgLighrB9t9gtUCe4UL%2F261SNPhxejqGbPWRCo92AHdTmU87vKKaGsJAWpYZVpNKVkW%2BdI7GDxmbb5QUjDQZuDfxFjB%2Bk4uGWEQyXbVPIp2mN2Mxrfiq2ufDlb7uXO3eSgJjWjh5vxZLRKTPWybqbW9fcTl3qUIgm1ZEvX0sr3pKwgLZA084PBQVzYiGwQP4fbUFRBhu%2FN%2FaGUWDHYaS%2FwgXTEvFPU4few2spdQeaDdAEiSwySEETpxG%2FaK4LWXYkZum5gd6Edj0LTA%2FIARBnaP83L9L4yaCMpnZ2OAFvJuhypX0nsLYwE9uS6H1Smr5RbMCO38FxyC2blFq1AHIDMA2kk5CYHXIABiJcgscUg4pIMu0cpSLwnJGm9ryTVAqXJS0jU%2BeISDWckGp1JosFUW2ckVxN6O%2Bbz5OS%2BgUi59BfB%2FBQdD74ZD%2F6RzntfykXaGwml8DAya4RB%2B%2Fgxnu3NHbN62VtpKfTna2EMhDxLK%2BFFWpoP5XfPdq%2Fi8Y%2FB95Al%2FyODV3CvkoRRSniZiEXPkkWiavCSMVM4ArgR5aC%2Ba5uBzAsWEtc3FX3WQuJ%2BIv2%2BtQA8L0PY9vskrsAzz3Fflrjc0yaunsxJ8CSu6rpWIPG7wUJElBiEILFkZ5YsOyQQg0uHjx9fsA%2FzZ1icMCT6W%2F5rd0kpE0%2BPOeO3ZyYxsMJFzcdrzgKiHBAc4TWsEvlgg%2FO8j0bU4gd4120lGJc65Pv6KfCXYi8egG0fi6fi3DI5j6ecBzOUO6egfO4fiCnlXKxBR3k3Tab98mejfNL3ROejfK7Qzqk8tkESyaTBE8hnp%2Fw4s9hnVPl8ej7ubb4c5Z51OcrjGcqHLxO%2BqIvpV6R80v%2B8G%2BV8qj829z2L%2FmLvZv8A"></iframe>


### 多个中断处理的方式：

+ 顺序处理
+ 根据优先级决定优先处理的指令



## 性能评估

> - Lecture01

### CPU - 性能

#### 衡量 CPU 性能的依据

$$
CPI =\frac{ \sum_{i=1}^n(CPI_i\times I_i)}{I_C},I_C = \sum_{i=1}^n I_i,
$$

$$
I_i 为某种指令的条数, CPI_i为某种指令的时钟周期数, I_C 为总的指令数,
$$

$$
 则 CPI 为每条指令的平均时钟周期数,
$$

$$
T = I_C \times CPI \times t, t 为时钟周期,
$$

$$
IPS(每秒钟总指令数) = \frac{f}{CPI} = \frac{I_C}{T} ,对应有MIPS，要 \times 10^{-6}
$$

$$
MIPS\ = \frac {I_c}{T \times 10^6 } = \frac {f}{ CPI \times 10^6 } 
$$

RAM - 容量与速度……

IO - 容量与速度……

BUS - 速度……

 ……

### 主要目标

CPU速度的提升