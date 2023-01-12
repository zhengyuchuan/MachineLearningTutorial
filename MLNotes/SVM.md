SVM(Support Vector Machine)支持向量机

1.梯度向量是二维曲面的法向量。

假设存在等高线F(x, y) = 0，三维曲面z = F(x, y)

根据全微分公式：
$$
dz = 0 = \frac {\partial{z}}{\partial {x}} dx + \frac {\partial{z}}{\partial {y}} dy
$$
可以看出向量$(\frac{\partial{z}}{\partial {x}}, \frac{\partial{z}}{\partial {y}})$与向量$(dx, dy)$垂直：

dx与dy是在等高线上随机取的，所以$(\frac{\partial{z}}{\partial {x}}, \frac{\partial{z}}{\partial {y}})$表示等高线的法向量





2.两个支持向量点之间距离

假设3个特征，两个支持向量点为$(x_1, y_1, z_1)$，$(x_2, y_2, z_2)$

假设超平面为：$w_1x + w_2y + w_3z + b= 0$，将超平面上下移动c，达到支持向量点，那么有：
$$
\begin{cases}
w_1x_1 + w_2y_1 + w_3z_1 + b &= c \\
w_1x + w_2y + w_3z + b &= 0 \\
w_1x_2 + w_2y_2 + w_3z_2 + b &= -c
\end{cases}
$$
对所有等式左右除以c。得：
$$
\begin{cases}
\frac{w_1x_1}{c} + \frac{w_2y_1}{c} + \frac{w_3z_1}{c} + \frac{b}{c} &= 1 \\
\frac{w_1x}{c} + \frac{w_2y}{c} + \frac{w_3z}{c} + \frac{b}{c} &= 0 \\
\frac{w_1x_2}{c} + \frac{w_2y_2}{c} + \frac{w_3z_2}{c} + \frac{b}{c} &= -1
\end{cases}
$$
可以将$\frac{w_1}{c}$，$\frac{b}{c}$这种变量调整下。得：
$$
\begin{cases}
w_1x_1 + w_2y_1 + w_3z_1 + b &= 1 \\
w_1x + w_2y + w_3z + b &= 0 \\
w_1x_2 + w_2y_2 + w_3z_2 + b &= -1
\end{cases}
$$
根据点到直线距离公式得，其中一点到超平面的距离：
$$
\begin{aligned}
d &= \frac{|w_1x_1 + w_2y_1 + w_3z_1 + b|}{\sqrt{w_1^2+w_2^2+w_3^2}} \\
 &= \frac{1}{||w||}

\end{aligned}
$$
那么支持向量之间的距离就是：
$$
2d = \frac{1}{||w||}
$$








