### 矩阵的加减乘

```python
A=np.mat([[3,-1],[1,0]])
B=np.mat([[-7,2],[3,5]])
A+B  #matrix([[-4,  1],[ 4,  5]])
A-B  #matrix([[10, -3],[-2, -5]])
A*B  #matrix([[-24,   1],[ -7,   2]])
B*A  #matrix([[-19,   7],[ 14,  -3]])
```

### 矩阵的逆

```python
A=np.mat([['a','b'],
         ['c','d']])
```

#### A的逆矩阵计算：

$$
A^{-1}=\frac{1}{ad-bc}\begin{bmatrix}d,-b\\-c,a\\\end{bmatrix}
$$

#### A的行列式：

$$
|A|=ad-bc
$$

#### 高斯消去法

原始矩阵
$$
\begin{bmatrix}1,0,1\\0,2,1\\1,1,1\\\end{bmatrix}
$$
画出单位矩阵：
$$
\begin{bmatrix}1,0,1\\0,2,1\\1,1,1\\\end{bmatrix}|\begin{bmatrix}1,0,0\\0,1,0\\0,0,1\\\end{bmatrix}
$$
对同行进行加减，或者替换、交换、以及两行之间相加减得到的结果替换某一行。
1.第三行减去第一行：
$$
\begin{bmatrix}1,0,1\\0,2,1\\0,1,0\\\end{bmatrix}|\begin{bmatrix}1,0,0\\0,1,0\\-1,0,1\\\end{bmatrix}
$$
2.第三行和第二行交换位置
$$
\begin{bmatrix}1,0,1\\0,1,0\\0,2,1\\\end{bmatrix}|\begin{bmatrix}1,0,0\\-1,0,1\\0,1,0\\\end{bmatrix}
$$
3.第三行减去第二行得到的结果替换第三行：
$$
\begin{bmatrix}1,0,1\\0,1,0\\0,0,1\\\end{bmatrix}|\begin{bmatrix}1,0,0\\-1,0,1\\2,1,-2\\\end{bmatrix}
$$
4.第一行减去第三行得到的结果替换第一行：
$$
\begin{bmatrix}1,0,0\\0,1,0\\0,0,1\\\end{bmatrix}|\begin{bmatrix}-1,-1,2\\-1,0,1\\2,1,-2\\\end{bmatrix}
$$
最终得到的右边的矩阵即为原始矩阵的逆

#### 矩阵法求解方程组

$$
3x+2y=7,
-6x+6y=6
$$



转换成矩阵就是：
$$
\underbrace{\begin{bmatrix}3,2\\-6,6\\\end{bmatrix}}_{A}\underbrace{\begin{bmatrix}x\\y\\\end{bmatrix}}_{B}=\underbrace{\begin{bmatrix}7\\6\\\end{bmatrix}}_{C}
$$
两边同时乘以矩阵A的逆：
$$
A^{-1}AB=A^{-1}C
\rightarrow
IB=A^{-1}C
\rightarrow
B=A^{-1}C
$$

```python
B=np.linalg.inv(np.mat([[3,2],[-6,6]]))*np.mat("7;6")
#matrix([[1.],[2.]])
```

### 奇异矩阵

首先，如果一个矩阵A存在另外一个矩阵B使得:
$$
AB=BA=I
$$

那么矩阵A是可逆的，称为非奇异矩阵。

那么找不到上述的矩阵B，则A称为奇异矩阵。也就是A不可逆
依据上述求逆方法，当矩阵A的项列式：
$$
|A|=ad-bc=0
$$
则矩阵A不可逆

### 向量

<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/vqRAf2.jpg' alt='vqRAf2'/>
所有可以表示为
给定向量线性组合的向量集合被称为

**给定向量张成的空间。**

对于大部分的二维向量，它们张成的空间是所有二维向量的集合，当它们 

**共线时，张成的空间就是终点落在一条直线上的向量的集合。**

那么怎么判断向量之间是否具有线性相关呢？
假设有向量：
$$
A=\begin{bmatrix}2\\1\\\end{bmatrix},B=\begin{bmatrix}4\\2\\\end{bmatrix}
$$

$$
B=2*A
$$

<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/I8usYe.jpg' alt='I8usYe'/>

### 向量线性相关定义

现有向量集合：$\{v_1,v_2,v_3....v_n\}$，若存在常数集合$c_i=\{c_1,c_2...c_n\}$，并且$\{c_1,c_2...c_n\}$不同时为0时，使得：$\\c_1*v_1+c_2*v_2+...c_n*v_n=0$，则表示向量线性相关，反之只有当$c_i$同时为0时，才能使等式成立，则表示线性无关

设：$S=\left\lbrace\begin{bmatrix}1\\-1\\2\\\end{bmatrix}\begin{bmatrix}2\\1\\3\\\end{bmatrix}\begin{bmatrix}-1\\0\\2\\\end{bmatrix}\right\rbrace$，是否有$c_1*\begin{bmatrix}1\\-1\\2\\\end{bmatrix}+c_2*\begin{bmatrix}2\\1\\3\\\end{bmatrix}+c_3*\begin{bmatrix}-1\\0\\2\\\end{bmatrix}=\begin{bmatrix}0\\0\\0\\\end{bmatrix}$

解三元一次方程得到：$c_1=c_2=c_3=0$。所以向量集合S为线性无关

### 线性子空间

学术定义：
1.设W是线性空间V的非空子集，则W是V的子空间的充要条件是：（1）若$\alpha,\beta \in W$，则$\alpha+\beta\in W$；（2）若$\alpha\in W,K\in R$，则$K\alpha\in W$。
我觉得一个很好的解释,来源知乎：[破魔之箭](https://www.zhihu.com/question/48849797/answer/115314179)

1.子空间之所以这样定义，其实和定义线性空间的思维模式是一样的，对于一个空间，我们希望空间内的元素经过线性组合之后仍然在该空间内**（封闭性）**，那么这样的空间就是一个线性（子）空间。如何能够实现线性组合仍在空间内呢？那么只要元素满足两条性质，就是你列的那两条。一个简单的推理：

 （1）假设$x_1$,$x_2$都在空间内，那么$K_1x_1$由性质2就知道也在空间内，相应的$K_2x_2$也在空间内，再有性质1就知道$K_1x_1+K_2x_2$在空间内，这样就证明了线性组合仍在空间内，而证明的基石就是列出的那两条性质。

  (2)体现出“子”的性质，其实就在于封闭性，这就是“子”的性质，那么你肯定会问这与原空间的定义有什么区别，其实没啥区别，原空间也是原空间的一个子空间，只不过这个子空间是最大的子空间，而最小的子空间是0空间，在这之间有一系列子空间，如直线，平面等等，唯一一点就是这些子空间的标志性特征在于它们都是封闭的线性空间，而类似两条直线或者两个平面构成的元素集就不可以称为一个子空间，其实稍微说得深一些，任何有限个子空间的并集都不可能构成原空间，这是外话。在学习线性代数的过程中，一定要牢牢把握线性组合这一概念，这是核心概念，也是标志着线性空间的核心性质。

2.子空间有很多的应用，但我觉得最广泛的应用还是来自于奇异值分解(SVD)，初学线性代数可能不会接触到这一方法，但是我可以直观地和你说明什么是奇异值分解以及其与子空间的关系。假如我们在三维空间内有一些离散分布的数据点，但是这些数据点近似分布在一个二维子平面内，可能有一些偏差，那么奇异值分解所做的就是寻找这个最佳的二维子平面，从而拟合三维空间的数据点分布，这种用子空间去拟合数据的方式实际上就是一般说的线性拟合方法，这里就涉及到了子空间，下面的图直观感受一下svd。
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/j9TUOz.jpg' alt='j9TUOz'/>

### 子空间的基

线性空间中基的概念很重要。比如一个子空间中的任意一个向量都可用一组基来表示，有些问题可以通过寻找一组合适的基而大大化简。

定义：如果线性空间X中的有限个向量张成X并且本身线性无关,则称他们为X的一组基(basis)。

下边对基的定义和性质做一些说明:

假设：由有限个向量$x_1,...,x_n$张成线性空间V有基.

证明：假设$x_1,...,x_n$线性相关。则存在一个$x_i$可以表示成其他向量的线性组合.把这个向量从向量组中剔除.则剩余的向量仍然可以张成线性空间X

重复这一步骤直到剩下的向量线性无关.显然他们仍然可以张成线性空间V 所以他们是线性空间V的一组基

### 向量的点积与长度

点积：
$$
\begin{bmatrix}a_1\\a_2\\...\\a_n\end{bmatrix}\ \cdot \  \begin{bmatrix}b_1\\b_2\\...\\b_n\end{bmatrix}=a_1*b_1+...+a_n*b_n
$$

$$
V=\begin{bmatrix}a_1\\a_2\\...\\a_n\end{bmatrix}
$$

长度计算公式：
$$
\|V\|=\sqrt{a_1^2+...+a_n^2}\\
\|V\|^2=V\cdot V
$$

同时:
$$
{V\cdot W}=W\cdot V\\
(v+W)\cdot X=V\cdot X+W\cdot X\\
(c*V)\cdot W=c*(V \cdot W)
$$

### 柯西不等式

$$
|\overrightarrow{x}\cdot \overrightarrow{y}|\le \|\overrightarrow{x}\|* \|\overrightarrow{y}\|
$$

证明：x,y均为非0向量，假设有函数p(t)表示某个向量的长度
$$
p(t)=\|ty-x\|^2
$$
有上面定义可知，向量长度>=0,所以：
$$
p(t)=(ty-x)\cdot (ty-x)\ge0
$$

$$
\Downarrow
$$

$$
p(t)=t^2y\cdot y-2t(x\cdot y)+x\cdot x\ge0
$$

简化：
$$
p(t)=t^2a-2bt+c\ge0
$$
根据抛物线方程，a>0,则开口向上，则函数在b/2a时取值最小，所以令：t=b/2a
$$
p(\frac{b}{2a})=c-\frac{b^2}{4a}\ge0
$$

$$
\Downarrow\\
4ac\ge b^2\\
\Downarrow\\
x^2y^2\ge (x\cdot y)^2 \\
\Downarrow\\
xy\ge x\cdot y
$$

所以当x=c*y时，其中c为常数，则：
$$
xy=x\cdot y
$$

### 三角不等式

$$
\|\overrightarrow{x}+\overrightarrow{y}\|\le \|\overrightarrow{x}\|+\|\overrightarrow{y}\|
$$

同上，当x=c*y且c>0时，上式相等

###  向量的夹角

<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/dVk9SL.jpg' alt='dVk9SL' width="50%"/>
$$
cos(\theta)=\frac{\overrightarrow{a}\cdot \overrightarrow{b}}{\|\overrightarrow{a}\|\|\overrightarrow{b}\|}$$

当a和b垂直的时候，则可以得到：

则称a与b是正交
$$
\overrightarrow{a}\cdot \overrightarrow{b}=0
$$
则称a与b是正交

### R3中的法向量与定义的平面

法向量是空间解析几何的一个概念，垂直于平面的直线所表示的向量为该平面的法向量。由于空间内有无数个直线垂直于已知平面，因此一个平面都存在无数个法向量（包括两个单位法向量）。
两个由0点出发的向量形成的平面，想象成三角形的一个边，那么法向量则垂直与这条边，同时由向量的减法可知：
$$
\overrightarrow{c}=\overrightarrow{a}-\overrightarrow{b}
$$
所以，法向量N垂直与c，则：
$$
\overrightarrow{c}\cdot \overrightarrow{N}=0
$$
则平面的方程就可以计算出，设：
$$
A=\begin{bmatrix}1\\2\\3\\\end{bmatrix},B=\begin{bmatrix}x\\y\\z\\\end{bmatrix},N=\begin{bmatrix}1\\3\\-2\\\end{bmatrix}
$$
则：
$$
(A-B)\cdot N=0
$$
### 外积

在R3中向量A，B的外积
$$
A\times B=C\\
$$
得到的C向量与A和B正交
在前面介绍了：
a与b的点积
$$
a\cdot b=\|a\|\|b\|cos(\theta)
$$
那么在R3中a与b的外积：
$$
a*b=\|a\|\|b\|sin(\theta)
$$
### 行简化阶梯形

1.首非零元所在列的其余元素是0

2.非零行最左边的首个非零元素，严格地比上面行的首个非零元素更靠右

3.全零行都在矩阵的底部

例如：
$$\left[\begin{array}{dd}
1&2&3\\
0&1&2\\
0&0&1\\
\end{array}
\right] ,
\left[\begin{array}{dd}
1&2&3&4\\
0&3&2&2\\
0&0&2&5\\
\end{array}
\right],
\left[\begin{array}{dd}
1&1&0&7&2\\
0&0&1&-2&2\\
\end{array}
\right]
$$
以下的就不是了：

$$
\left[\begin{array}{dd}
1&2&3\\
0&1&2\\
0&1&1\\
\end{array}
\right],
\left[\begin{array}{dd}
1&2&3&4\\
0&3&2&2\\
0&0&0&0\\
0&0&2&5\\
\end{array}
\right]
$$

第一个是因为第三列的首个非0元素，没有在第二列首个非0元素的右边

第二个是因为全0列应该在矩阵底部

行简化矩阵的主元列，**主元是在主元位置上的非零元素**，上述矩阵的主元列依次是前三列，前三列，第一列和第三列，其他变量就是自由变量。

### 矩阵的线性组合

$$
a=\begin{bmatrix}3\\2\\-1\\\end{bmatrix},
b=\begin{bmatrix}2\\-1\\-3\\\end{bmatrix},
c=\begin{bmatrix}-1\\5\\3\\\end{bmatrix}\\
A=\begin{bmatrix}a\\b\\c\\\end{bmatrix},
X=\begin{bmatrix}x_1\\x_2\\x_3\\\end{bmatrix}
$$

$$
AX=ax_1+bx_2+cx_3
$$

### 零空间和齐次线性方程组

零空间也称为线性映射的核，不同于行、列空间关注的Ax=b,零空间$N(A)$关注的是x的空间，即改空间中的任何向量都是齐次线性方程组$Ax=0$的解。

举例：

$$
\begin{bmatrix}1,1,2\\1,2,3\\1,3,4\\1,4,5\\\end{bmatrix} \begin{bmatrix}x_1\\x_2\\x_3\\\end{bmatrix}=\begin{bmatrix}0\\0\\0\\0\\\end{bmatrix}
$$
可以看到左边向量的第三列=第一列+第二列，所以很容易得到一个解$\begin{bmatrix}1\\1\\-1\\\end{bmatrix}$，所以任意的$C\begin{bmatrix}1\\1\\-1\\\end{bmatrix}$，$C$是常数，都是上述的解。

因此$C\begin{bmatrix}1\\1\\-1\\\end{bmatrix}$便是A的零空间，记为$N(A),N(A)\in R^n$

### 非齐次线性方程组

零空间在求解非齐次线性方程组（Non-homogeneous systems of linear equations）$Ax=b$中起到重要作用

设：$u,v$是非齐次线性方程组$Ax=b$的两个解，那么$A(u-v)=Au-Av=b-b=0$,所以$u-v$位于A的零空间中，则$Ax=b$的完整解可以表述为$(v+z)$,$z$是$Ax=0$的零空间$N(A)$。

用几何语言来描述就是：Ax=b的解是在v的基础上平移A的零空间

### 四个子空间汇总：

所有的一切从一个向量A开始说起：
$$
A=\begin{bmatrix}1,1,1,1\\2,1,4,3\\3,4,1,2\\\end{bmatrix}
$$
Q:A的列空间是？
$$
C(A)=span\left(\begin{bmatrix}1\\2\\3\\\end{bmatrix},\begin{bmatrix}1\\1\\4\\\end{bmatrix},\begin{bmatrix}1\\4\\1\\\end{bmatrix},\begin{bmatrix}1\\3\\2\\\end{bmatrix}\right)
$$

Q:A的零空间是？

A的零空间=A的行简化阶梯型的零空间：$N(A)=N(rref(A))=\begin{bmatrix}x_1\\x_2\\x_3\\x_4\\\end{bmatrix}$

A的行简化阶梯型：
$$
\hat{A}=\begin{bmatrix}1&0&3&2\\0&1&-2&-1\\0&0&0&0\\\end{bmatrix}
$$
所以
$$
\left(\hat{A}*\begin{bmatrix}x_1\\x_2\\x_3\\x_4\\\end{bmatrix}=\begin{bmatrix}0\\0\\0\\\end{bmatrix}\right)\\
\Downarrow\\
x_1=-3x_3-2x_4\\
x_2=2x_3+x_4\\
\Downarrow\\
N(A)=\begin{bmatrix}x_1\\x_2\\x_3\\x_4\\\end{bmatrix}=x_3\begin{bmatrix}a_1\\a_2\\a_3\\a_4\\\end{bmatrix}+x_4\begin{bmatrix}b_1\\b_2\\b_3\\b_4\\\end{bmatrix}
$$
由上面的$x_1,x_2$的线性公式变换成矩阵可以知道，$a_1=-3,b_1=-2,a_2=2,b_2=1$，在A的行简化阶梯型矩阵中，第一列和第二列的1为主元，第三列和第四列没有主元，所以$x_3,x_4$是自由变量，则$a_3=1,a_4=0，b_3=0,b_4=1$

最后得出：
$$
N(A)=\begin{bmatrix}x_1\\x_2\\x_3\\x_4\\\end{bmatrix}=x_3\begin{bmatrix}-3\\2\\1\\0\\\end{bmatrix}+x_4\begin{bmatrix}-2\\1\\0\\1\\\end{bmatrix}=span\left(\begin{bmatrix}-3\\2\\1\\0\\\end{bmatrix},\begin{bmatrix}-2\\1\\0\\1\\\end{bmatrix}\right)
$$

Q:A是线性无关的吗？
当向量线性无关的时候$N(A)=\{\vec{0}\}$，但是由上面可知$N(A)$是有其他的解，所以$N(A)$不是线性相关的


Q:A是否是A的列空间的一组基？
既然是线性相关的，那就不是A的基，表示A内有多余的向量，是可以由其他的向量生成的。所以两个自由向量是可以由两个主元向量生成的。
$$
x_1\begin{bmatrix}1\\2\\3\\\end{bmatrix}+x_2\begin{bmatrix}1\\1\\4\\\end{bmatrix}+x_3\begin{bmatrix}1\\4\\1\\\end{bmatrix}+x_4\begin{bmatrix}1\\3\\2\\\end{bmatrix}=0
$$
证明：令$x_3=0,x_4=-1$解出$x_1,x_2$则说明第四列是可以由前两列线性组合生成的，再令$x_3=-1,x_4=0$解出$x_1,x_2$，则说明第三列是可以由前两列线性组合生成的。所以最后只剩下第一列和第二列，这就是A的列空间的基。

概要：

（1）任意子空间的基底数目相同

（2）任意一个矩阵的零度=行简化阶梯型矩阵的自由变量的数目

（3）矩阵的秩(Rank)=行简化阶梯型矩阵的主元的数目

### 线性变换

Q:满足什么条件可以叫做线性变换：
$$
T(\vec{a}+\vec{b})=T(\vec{a})+T(\vec{b})\\

T(c\vec{a})=cT(\vec{a})
$$
所有线性变换都可以携程矩阵与向量的乘积。

#### 变换的像空间

$\vec{v}$是$R^n$的子空间，$\vec{a},\vec{b}\in \vec{v}$,$T(v)=im(v)$是v在T变换下的像,那么$im($v)包含V下所有子集的T变换的像。
那么意味着：
$$
T(\vec{a}),T(\vec{b})\in T(v)\\T(\vec{a}+\vec{b})=T(\vec{a}+\vec{b})\in T(\vec{v})
$$
反过来，如果知道线性转换T(x)->Y和已知Y下的像S，那么对应的在X下形成S的子集，称为原像,记作：$T^{-1}(s)$

#### 线性变换的加法和数乘运算

$$
S:R^n\rightarrow R^m，T:R^n\rightarrow R^m\\
\Downarrow\\
(S+T)\vec{x}=S(\vec{x})+T(\vec{x})，（S+T):R^n\rightarrow R^m\\
\Downarrow\\
(cS)\vec{x}=c(S(\vec{x}))，cS:R^n\rightarrow R^m
$$

#### 线性变换：放缩和映射

假设：
$$
\vec{a}=\begin{bmatrix}3\\2\\\end{bmatrix},\vec{b}=\begin{bmatrix}-3\\2\\\end{bmatrix},\vec{c}=\begin{bmatrix}3\\-2\\\end{bmatrix}
$$
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/kMnC7h.jpg' alt='kMnC7h'/>
想要将上图变换成下图
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/p2coJC.jpg' alt='p2coJC'/>

对比原图形，可以看出x轴进行了反转，y轴扩大了2倍。转换成函数表示即：
$$x_1=-1x，y_1=2y$$
$$\Downarrow$$
$$
T(\begin{bmatrix}x\\y\\\end{bmatrix})=\begin{bmatrix}-x\\2y\\\end{bmatrix}
$$

从R2的单位矩阵出发，进行变换。对单位矩阵的每一列进行变换
$$A=\left[T(\begin{bmatrix}1\\0\\\end{bmatrix})T(\begin{bmatrix}0\\1\\\end{bmatrix})\right]=\begin{bmatrix}-1,0\\0,2\\\end{bmatrix}$$
那么$\vec{a}$经过变换之后就等于
$$\begin{bmatrix}-1,0\\0,2\\\end{bmatrix}\begin{bmatrix}-3\\2\\\end{bmatrix}=\begin{bmatrix}3\\4\\\end{bmatrix}$$
依次变换之后得到的坐标，就是目标点的坐标了。

### 单位向量

$$
\hat{i}=\begin{bmatrix}1,0,0\\0,1,0\\0,0,1\\\end{bmatrix}
$$

已知一个向量求这个向量的单位向量：
$$
A=\begin{bmatrix}2\\1\\\end{bmatrix}\\
\hat{u}=\sqrt{2^2+1^2}\begin{bmatrix}2\\1\\\end{bmatrix}\\
\hat{u}=\begin{bmatrix}\frac{2}{\sqrt{5}}\\\frac{1}{\sqrt{5}}\\\end{bmatrix}
$$

## 投影

已知向量x和方向L，x减去x在L上的投影将与L正交。

<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/g8m6IG.png' alt='g8m6IG' width="50%"/>

即：
$(\vec{x}-c\vec{v})\cdot \vec{v}=0$，v是方向L上的向量，所以$L=c\vec{v}$，最后得到：
$$
c=\frac{\vec{x}\cdot \vec{v}}{\vec{v}\cdot \vec{v}}
$$
那么
$$
Proj_l(\vec{x})=\left(\frac{\vec{x}\cdot \vec{v}}{\vec{v}\cdot \vec{v}}\right)\vec{v}
$$
定义$\hat{u}$是$\vec{v}$上的单位向量，那么上面的公式可以表示为：
$$
Proj_l(\vec{x})=\left(\frac{\vec{x}\cdot \hat{u}}{\hat{u}\cdot \hat{u}}\right)\hat{u}\\
\downarrow\\
Proj_l(\vec{x})=(\vec{x}\cdot \vec{u}) \vec{u}=A\vec{x}\\
从R2->R2中。\\
A=\begin{bmatrix}1,0\\0,1\\\end{bmatrix}\begin{bmatrix}u_1\\u_2\\\end{bmatrix}=\begin{bmatrix}u_1^2,u_2u_1\\u_1u_2,u_2^2\\\end{bmatrix}
$$
示例：
设：$L=\begin{bmatrix}2\\1\\\end{bmatrix}$，那么$\vec{x}$在L上的投影就等于：
$$
Proj_l(\vec{x})=\begin{bmatrix}\frac{4}{5},\frac{2}{5}\\\frac{2}{5},\frac{1}{5}\\\end{bmatrix}\vec{x}
$$
当矩阵$\vec{x}$经过S变换得到$\vec{y}$再经过T变换得到$\vec{L}$。$\vec{y}=A\vec{x}，\vec{L}=B\vec{y}$
那么最终的复合变换矩阵就变成了：$\vec{L}=AB\vec{x}$
所以，复合矩阵的变换变成了两个矩阵的乘积。

### 逆函数

首先恒等函数表述,总是返回值自身
$$
I(x)=x
$$
假设有函数$f(x)=y$，并且其可逆,那么函数$f$的逆函数表示为$f^-1$，并且$f。f^-1=I$

$f(x)$的解是唯一的，并且是可逆的那么：
（1）$f^{-1}是唯一的$

（2）$f(x)=y的解是唯一的$

### 满射函数和单射函数

$f(x)=Y$在Y中每一个y至少都有一个对应的x，使得$f(x)=y$那么就是满射函数，
上域是可以映射到的集合，不一定每个都要映射到。值域是你必须要映射到的集合（im，range)。
在Y中每一个y只有一个对应的x，使得$f(x)=y$那么就是单射函数

满射函数和单射函数并不是互斥的，当一个函数即是满射函数，又是单射函数，那么这个函数是可逆的。因为$f(x)$的解是唯一的。

#### 变换是否映上的判别方法：

$$
Rank(A)=dim(C(A))
$$

示例：

$s$是映上的吗？
对S进行行简化阶梯形得到：
$$\begin{bmatrix}1\quad0\\0\quad1\\0\quad0\\\end{bmatrix}$$
可以看到矩阵中只有两个主元。那么
$$Rank(\begin{bmatrix}1\quad2\\3\quad4\\5\quad6\\\end{bmatrix})=2\quad!=R^3$$
所以没有映上。
### 可逆性的简化条件及求逆
$$T:R^n-R^n \quad T(x)=A_(n*n)\vec{x}$$
只有当$T$的行简化阶梯矩形等于$I_n$的单位矩阵，那么T是可逆的
那么如果一个矩阵是可逆的，如何求得其逆矩阵呢？（高斯-若尔丹消元法）
$$A=\begin{bmatrix}1&-1&-1\\-1&2&3\\1&1&4\\\end{bmatrix}$$
首先写上对应的n*n的单位矩阵：
$$\left[\begin{array}{ccc|ccc}1&-1&-1&1&0&0\\-1& 2&3&0&1&0\\1&1&4&0&0&1\\\end{array}\right]$$
直到把左边消成单位矩阵，那么右边的矩阵就变成了A的逆矩阵了。
$$\left[\begin{array}{ccc|ccc}1&0&0&5&3&-1\\0&1&0&7&5&-2\\0&0&1&-3&-2&1\\\end{array}\right]$$
$$\Downarrow$$
$$A^{-1}=\left[\begin{array}{ccc|ccc}5&3&-1\\7&5&-2\\-3&-2&1\\\end{array}\right]$$

### 萨吕法则求行列式

$$
A=\begin{bmatrix}a&b&c\\d&e&f\\g&h&i\\\end{bmatrix}
$$

首先复制前两列进行增广：
$$
\left[\begin{array}{ccc|cc}a&b&c&a&b\\d&e&f&d&e\\g&h&i&g&h\\\end{array}\right]
$$

$$
|A|=aei+bfg+cdh-ceg-afh-bdi
$$

当矩阵中某一行乘以$K,K\in R$时，$det(A^{'})=k*det(A)$，如果矩阵整体乘以K，则$det(A^{'})=k^2*det(A)$

三个矩阵A,B,C当C中某一行$Row(c)=Row(A)+Row(B)$，并且其他行全部相等时，$det(C)=det(A)+det(B)$
$$
A=\begin{bmatrix}r_1\\r_2\\r_i\\r_j\\\vdots\\r_n\\\end{bmatrix}
$$
当交换$r_i,r_j$的位置时得到$S$，那么：
$det(S)=-det(A)$,**当$r_i,r_j$相同时，则表示$det(S)=-det(A)=det(A)$,说明行列式=0，则矩阵不可逆。**

上三角矩阵$A=\begin{bmatrix}1,2,3\\0,2,1\\0,0,4\\\end{bmatrix}$的行列式即对角线的乘积：$det(A)=1*2*4$

现有向量$\vec{a}=[0,3],\vec{b}=[4,0]$可以看成两个向量,形成了矩形的面积$S=3*4$

<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/wZUoru.jpg' alt='wZUoru'/>

对两个向量进行T变换，$T(\vec{x})=\begin{bmatrix}a&b\\c&d\\\end{bmatrix}\vec{x}$,对上述四个点进行变换，得到新的点形成的四边形B，形成的面积是？
$$
T([0,0])=[0,0]\\
T([3,0])=[3a,3c]\\
T([3,4])=[3a+4b,3c+4d]\\
T([0,4])=[4b,4d]
$$
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/mLeEiA.jpg' alt='mLeEiA'/>

**四边形的面积=abs(矩阵的行列式)**

$S(B)=\left|\begin{bmatrix}3a&4b\\3c&4d\\\end{bmatrix}\right|=abs(12ad-12bc)=abs(12(det(A)))$

### 矩阵的转置
```
a=[[1 2]
 [4 3]]
-----
a`=[[1 4]
 [2 3]]
```
#### 矩阵转置之后的行列式
设矩阵$A_{n*m}$的矩阵，那么$A^T$就是$A_{m*n}$，同时$det(A)=det(A^T)$
矩阵乘积的转置
矩阵$A*B=B^T*A^T$，$(AB)^T=B^T*A^T$，
#### 转置矩阵的加法和求逆
$$(A+B)^T=A^T+B^T,(A^T)^{-1}=(A^{-1})^T$$

### 四个基本子空间汇总

对于一个$m*n$的矩阵A，其有四个基本空间：
* 列空间$C(A)$：

    定义：列空间是矩阵A的列向量线性组合构成的空间，对于矩阵A涞水，每个列向量有m个分量，即列空间是属于$R^m$的子空间
    
    基：矩阵A化简到最简矩阵时有主元r，则秩也为r，主元列就是列向量的一组基。
   
    维数：列空间的空间维数为r
    
* 零空间$N(A)$:
  
    定义：即$Ax=0$的解构成的空间，Ax在本质上属于线性组合，A一共有n个列向量，所以零空间是$R^n$的子空间
    
    基：A的秩(主元数)为r，则自由列为n-r列，就构成了零空间的n-r个基向量
    
    维数：n-r
    
* 行空间$C(A^T)$

    定义：行空间是矩阵A的行向量线性组合构成的空间，也可以理解为A转置的列空间，即$C(A^T)$。对于$m*n$的矩阵A来说，每个行向量有n个分量，即行空间属于$R^n$的子空间。

    基：A的行空间可以看成是$A^T$的列空间，也可以就是化简到最简矩阵的时候主元列就是行空间的基。

    维数：行空间的维数也是秩r


* 左零空间$N(A^T)$:

    设$A=\begin{bmatrix}2&-1&-3\\-4&2&6\\\end{bmatrix}$，转换为行最简阶梯矩阵得到 $\begin{bmatrix}1&-1/2&-3/2\\0&0&0\\\end{bmatrix}$，可以看到只有第一列是主元，也就是主向量$C(A)=span(\begin{bmatrix}2\\-4\\\end{bmatrix})$

    只有一列主元，也表示$Rank(A)=1$。矩阵的秩、列空间的基向量数、独立向量数、主元数，这些都是一个意思。

    A的零空间：
    $$\begin{bmatrix}2&-1&-3\\-4&2&6\\\end{bmatrix}\begin{bmatrix}x_1\\x_2\\x_3\\\end{bmatrix}=\begin{bmatrix}0\\0\\0\\\end{bmatrix}$$
    $$\Downarrow$$
    $$x_1=\frac{x_2}{2}+\frac{3x_3}{2}$$
    $$\Downarrow$$
    $$\begin{bmatrix}x_1\\x_2\\x_3\\\end{bmatrix}=\begin{bmatrix}\frac{1}{2}\\1\\0\\\end{bmatrix}*x_2+\begin{bmatrix}\frac{3}{2}\\0\\1\\\end{bmatrix}*x_2$$
    $$\Downarrow$$
    $$N(A)=span\left(\begin{bmatrix}\frac{1}{2}\\1\\0\\\end{bmatrix},\begin{bmatrix}\frac{3}{2}\\0\\1\\\end{bmatrix}\right)$$

    上面求解的零空间求的是$Ax=\vec{0}$的解，那么转置之后的A呢也就是$A^Tx=\vec{0}$的解。上述同样的操作过后得到：
    $$\begin{bmatrix}1&-2\\0&0\\0&0\\\end{bmatrix}\begin{bmatrix}x_1\\x_2\\\end{bmatrix}=\vec{0}$$
    $$\Downarrow$$
    $$\begin{bmatrix}x_1\\x_2\\\end{bmatrix}=\begin{bmatrix}2\\1\\\end{bmatrix}x_2$$
    所以：
    $$N(A^T)=span(\begin{bmatrix}2\\1\\\end{bmatrix})$$

    现在我们把两边同时转置：
    $$(A^Tx)^T=\vec{0} \Rightarrow x^T(A^T)^T=x^TA=\vec{0}$$
    可以看到对比之前$Ax=\vec{0}$，现在变换成了$x^TA=\vec{0}$，由于$x^T$在A的左边，所以也叫做A的**左零空间**。
	![四个子空间关系](https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/l28p9z-20210324173849592.jpg)
### 正交以及正交补
![gaCv7X](https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/gaCv7X-20210324173849658.png)
![m7S39l](https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/m7S39l.jpg)


$V是A_{n\times k}的子空间，那么dim(C(A))+dim(N(A^T))=n$

**$R^n$中的任何向量可以用零空间N(A)中的向量与行空间$C(A^T)$中的向量的和$**

### Ax=b的行空间中的解
$A_{m\times n}=\begin{bmatrix}a_1&a_2&a_3\dots a_n\\\end{bmatrix}，\vec{b}\in C(A)$

<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/s8OeWM.jpg' alt='s8OeWM' width='50%'>

根据上面的定义，可知将$\vec{x}$拆解成$\vec{x}=\vec{r}+\vec{n}$,得到$A(\vec{r}+\vec{n})=\vec{b}$，由于$\vec{n}$是零向量里的，所以$A\vec{n}=0$，也就是$A\vec{r}=\vec{b}$,$\vec{r}$也就是行向量里的子空间。

结论：假设有一个向量$\vec{b}\in C(A)$，那么Ax=b的最小解是A的行空间中的唯一元素 $\vec{r}|r\in C(A^T)$
举例：
$$A=\begin{bmatrix}
 3& -2&\\
 6& -4& 
\end{bmatrix},
\vec{b}=
\begin{bmatrix}
9\\ 
18
\end{bmatrix}$$
首先求零空间N(A)=N(rref(A))
$$\begin{bmatrix}
 3& -2\\
 0& 0
\end{bmatrix}
\begin{bmatrix}
x_1\\ 
x_2
\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$$
$$\Downarrow$$
$$N(A)=\begin{bmatrix}2\\3\end{bmatrix}$$

求Ax=b的解，先建立增广矩阵
$$\left[\begin{array}{cc|c}
 3& -2&9\\
 0& 0& 18
\end{array}\right] \Rightarrow \begin{bmatrix}
 3& -2\\
 0& 0
\end{bmatrix}
\begin{bmatrix}
x_1\\ 
x_2
\end{bmatrix}=\begin{bmatrix}3\\0\end{bmatrix}$$
$$\Downarrow$$
所以Ax=b的解集就是
$$\begin{bmatrix}
3\\ 
0
\end{bmatrix}+c\begin{bmatrix}
2\\ 
3
\end{bmatrix}\mid c\in R^n$$

行空间：
$$C(A^T)=span\left(\begin{bmatrix}
3\\ 
-2
\end{bmatrix},\begin{bmatrix}
6\\ 
-4
\end{bmatrix}\right)$$
可以看到第二列是第一列的倍数，所以舍去。得到
$$span\left(\begin{bmatrix}
3\\ 
-2
\end{bmatrix}\right)形成的张成空间就是行空间$$
上述三个张成空间形成的图：
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/0j2Kgc.jpg' alt='0j2Kgc'/>
那么上面说的Ax=b的在行空间中的最小解就是行空间与解集的交点。

### 投影
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/g8m6IG.png' alt='g8m6IG' width="50%"/>

由上图可以看出向量$\vec{x}$在平面L上投影$\vec{v}$与L的正交$\vec{w}=\vec{x}-\vec{v}$构成一个直角三角形，所以$\vec{x}-\vec{w}$得到$Proj_L^x$。$\vec{w}$也可以看作是$\vec{x}$在平面L的正交补$L^{\perp}$上的投影，即$Proj_{L^{\perp}}^x$
由上图可以看出向量$\vec{x}$在平面L上投影$\vec{v}$与L的正交$\vec{w}=\vec{x}-\vec{v}$构成一个直角三角形，所以$\vec{x}-\vec{w}$得到$Proj_L^x$。$\vec{w}$也可以看作是$\vec{x}$在平面L的正交补$L^{\perp}$上的投影，即$Proj_{L^{\perp}}^x$

###  子空间上的投影的求解
$$Proj_L^v=A(A^TA)^{-1}A^T\vec{x}$$
**投影是子空间中距离原向量最近的向量。**

### 最小二乘逼近
当$Ax=\vec{b}$有解的时候，我们可以说$\vec{b}$在A的列空间上，但是当$Ax=\vec{b}$无解的时候，如下图所示：
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/CAWnS1.png' alt='CAWnS1' width="50%"/>

在上一节中我们直到，投影是空间中举例原向量最近的向量，那么$Ax=\vec{b}$无解的时候，我们求$Ax=\vec{b}$的最近解，就是*最小二乘解*。
设我们最小二乘解是$x^{'}$:

$$Ax^{'}=Proj_{C(A)}^b$$
$$\Downarrow$$
$$Ax^{'}-\vec{b}=Proj_{C(A)}^b-\vec{b}$$
$$Ax^{'}-\vec{b}\in C(A)^{\perp} \rightarrow Ax^{'}-\vec{b}\in N(A^T)$$
$$\Downarrow$$
$$A^T(Ax^{'}-\vec{b})=\vec{0}$$
$$\Downarrow$$
$$A^TAx^{'}=A^T\vec{b}$$
所以，当$Ax=\vec{b}$无解的时候，$A^TAx^{'}=A^T\vec{b}$求出的$x^{'}$就是使得$\vec{b}和Ax$的距离最小。这就是最小二乘解
举例：
在坐标系中共有四个点：(-1,0),(0,1),(1,2),(2,1),现在无法拟合一条直线穿过四个点，那么是否能找到或者拟合一条线使得四个点到这条直线的距离*也就是向量的长度，$\|x\|^2$*的和最短，也就是我们所要的最优解，（在线性回归中经常看到）。
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/ZQTV6l.png' alt='ZQTV6l' width="50%"/>
首先在2维中的直线方程，我们设方程为：$y=mx+b$,那么就有：
$$f(0)=-m+b,f(1)=b,f(2)=m+b,f(1)=2m+b$$
可以看到在上述方程组中，m和b并没有解。所以我们使用最小二乘法来拟合这个方程，转换成矩阵：
$$\begin{bmatrix}
-1 &1 \\ 
0 &1 \\ 
 1&1 \\ 
 2& 1
\end{bmatrix}\begin{bmatrix}
m\\ 
b
\end{bmatrix}=\begin{bmatrix}
0\\ 
1\\ 
2\\ 
1
\end{bmatrix}$$
根据我们的公式，$A^TAx^{'}=A^T\vec{b}$
$$\begin{bmatrix}
-1 &0&1&1\\ 
1&1&1&1& 
\end{bmatrix}\begin{bmatrix}
-1 &1 \\ 
0 &1 \\ 
 1&1 \\ 
 2& 1
\end{bmatrix}x^{'}=\begin{bmatrix}
-1 &0&1&1\\ 
1&1&1&1& 
\end{bmatrix}\begin{bmatrix}
0\\ 
1\\ 
2\\ 
1
\end{bmatrix}$$
$$\Downarrow$$
$$x^{'}=\begin{bmatrix}
\frac{2}{5}\\ 
\frac{4}{5}\\ 
\end{bmatrix}$$
所以最后拟合出来的直线方程就是$y=\frac{2}{5}x+\frac{4}{5}$

### 向量在不同基下的变换
V是$R^n$的子空间，$B=\begin{Bmatrix}
\vec{v_1} &\vec{v_2}&\cdots &\vec{v_k}
\end{Bmatrix},\vec{a}\in V \rightarrow \vec{a}=c_1\vec{v_1}+\cdots +c_k\vec{v_k}$,那么$c_1,c_2\cdots c_k就是a在基地B下的坐标,记作[\vec{a}]_B=\begin{bmatrix}
c_1\\ 
c_2\\ 
\vdots\\ 
c_k
\end{bmatrix}$,像$\begin{bmatrix}
1\\ 
0
\end{bmatrix},\begin{bmatrix}
0\\ 
1
\end{bmatrix}这种就叫做标准基$
对于不同的基坐标，向量的变换遵循：
$$C[\vec{a}]_B=\vec{a}$$
举例：
$张成空间V有一组基：\vec{v_1}=\begin{bmatrix}
1\\ 
2\\
3
\end{bmatrix},\vec{v_2}=\begin{bmatrix}
1\\ 
0\\
1
\end{bmatrix},[\vec{a}]_B=\begin{bmatrix}
7\\ 
-4
\end{bmatrix}$

$这样根据上面的公式就可以计算出B的标准坐标了。反之当我们已知a的标准坐标想要求得[x]_B的坐标$
$$[x]_B=C^{-1}\vec{x}$$

### 标准正交基
$B=\{\vec{v_1},\vec{v_2}\cdots \vec{v_k}\},B中的每一个向量长度为1，每个向量之间彼此正交，这就是B的标准正交基$

$A是V上的一个标准正交基，那么\vec{x}在V上投影矩阵公式：$
$$Proj_v^\vec{x}=AA^T\vec{x}$$

$B是V上的一个标准正交基，\vec{x}\in V，那么\vec{x}=c_1v_1+c_2v_2+\cdots c_kv_k，\vec{v_i}与\vec{x}的点乘$
$\vec{v_i}\cdot \vec{x}=c_1v_1v_i+c_2v_2v_i+\cdots+ c_iv_iv_i+\cdots c_kv_kv_i$
由标准正交基的特性可知，互相之间正交，自身长度为1，所以最后得到$\vec{v_i}\cdot \vec{x}=C_i$

$前面说的当我们已知a的标准坐标想要求得[x]_B的坐标，根据公式[x]_B=C_i\vec{x}$，在标准正交基下，可以简化成：

$$[x]_B=\begin{bmatrix}
\vec{v_1}\cdot \vec{x}\\ 
\vec{v_2}\cdot \vec{x}\\ 
\vdots \\ 
\vec{v_k}\cdot \vec{x}
\end{bmatrix},v_1,v_2是B上的一组标准正交基$$

### 施密特过程
在一个平面，或者三维空间中，任意一点都可以被坐标系表示出来。而我们更喜欢的是单位直角坐标系，因为在一个单位直角坐标系中，任意一个向量的坐标分量，通过简单的投影就可以搞定。施密特过程就是将任意坐标系变成直角坐标系的过程
<img src='https://cdn.jsdelivr.net/gh/caoliang12121/pic@master/uPic/uk3ycK.png' alt='uk3ycK' width="30%"/>

$\begin{Bmatrix}
v_1& v_2 & \cdots & v_k
\end{Bmatrix}$是V的一组基。

$V_1=span(\vec{v_1}),\vec{v_1}$的标准基$\vec{u_1}=\frac{\vec{v_1}}{\|\vec{v_1}\|}$

$V_2=span(\vec{v_1},\vec{v_2})=span(\vec{u_1},\vec{v_2})，并且\vec{v_1},\vec{v_2}是线性无关的，所以\vec{v_2}可以用c\vec{u_1}+d\vec{v_1^\perp}来表示，c\vec{u_1}其实就是前面所说的\vec{v_2}在\vec{v_1}上的投影Proj_{v_1}^{v_2}。$

$在已知\vec{v_1}的标准基\vec{u_1}时，Proj_{v_1}^{v_2}=(\vec{v_2}\cdot \vec{u_1})\vec{u_1}$

$那么令\vec{y_2}=\vec{v_2}-(\vec{v_2}\cdot \vec{u_1})\vec{u_1},\vec{v_2}的标准基\vec{u_2}=\frac{\vec{y_2}}{\|\vec{y_2}\|}$

$所以最后形成的张成空间可以表示成两个标准正交向量形成的空间span(\vec{u_1},\vec{u_2})$

$当扩展至三维后Proj_{v_2}^{v_3}=(\vec{v_3}\cdot \vec{u_1})\vec{u_1}+(\vec{v_3}\cdot \vec{u_2})\vec{u_2}=\vec{y_3},然后再标准化\vec{u_3}=\frac{\vec{y_3}}{\|\vec{y_3}\|}，形成span(\vec{u_1},\vec{u_2},\vec{u_3})的张成空间。$
依次扩展至N维。

### 特征向量、特征值、特征空间

假设有一个转换使得：$T(\vec{x})=\lambda \vec{x}，那么  \lambda \in R 被称为特征值，\vec{x}被称为特征向量$，在前面我们直到转换是一种线性变换，$T(\vec{x})=A\vec{x}$。

$$T(\vec{x})=\lambda \vec{x}=A\vec{x}，A是一个变换矩阵，\lambda 是一个常数，\vec{x}是非0向量$$

$$\lambda \vec{x}-A\vec{x}=\vec{0} \rightarrow (\lambda-A)\vec{x}=\vec{0}$$

$A是一个矩阵，\lambda 是一个常数,所以将\lambda 乘以A的单位矩阵I_n,得到(\lambda I_n-A)\vec{x}=\vec{0}，\vec{x}是非0向量所以\lambda I_n-A=\vec{0},最终得到\lambda I_n-A的行列式为0，即：$

$$det(\lambda I_n-A)=0$$

再根据$\lambda \vec{x}=A\vec{x}$即可求出特征向量

$\lambda I_n-A所形成的空间被称为特征空间E_{\lambda}=N(\lambda I_n-A)，对于不同的\lambda 有对应的不同的特征空间,$

### 向量的三重积展开
$$\vec{a}\times (\vec{b}\times\vec{c})=\vec{b}(\vec{a}\cdot \vec{c})-\vec{c}(\vec{a}\cdot \vec{b}$$

### 点到平面的距离
$$d=\frac{Ax_0+By_0+Cz_0-D}{\sqrt{A^2+B^2+c^2}}$$
已知平面方程为Ax+By+Cz=D和点坐标$P(x_0,y_0,z_0)$,则点到平面的距离可以通过上式算出。

顺带一句，点到直线的距离为：
$$d=\frac{Ax_0+By_0+C}{\sqrt{A^2+B^2}}$$