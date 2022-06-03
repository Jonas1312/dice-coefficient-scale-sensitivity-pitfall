# Dice Coefficient and Its Sensitivity to Scale

$$Dice = 2\frac{|Y\cap \hat{Y}|}{|Y| + |\hat{Y}|}$$

Where $|Y|$ is the ground truth and $|\hat{Y}|$ the estimate or prediction.

Let's name $r$ the number of pixels removed by the estimate, that is the number of false negatives FN:

$$|Y\cap \hat{Y}| = |Y| - r, \quad r\in[0, |Y|]$$

Same thing for the number of pixels added $a$ by the estimate, that is the number of false positives FP:

$$|Y\cup \hat{Y}| = |Y| + a, \quad a\in[0, |\hat{Y}|]$$

We thus have:

$$\begin{equation}
\begin{split}
Dice & = 2\frac{|Y\cap \hat{Y}|}{|Y| + |\hat{Y}|} \\
 & = 2\frac{|Y\cap \hat{Y}|}{|Y\cap \hat{Y}| + |Y\cup \hat{Y}|} \\
 & =2\frac{|Y| - r}{2|Y|-r+a} \\
 & =\frac{2|Y| - 2r}{2|Y|-r+a}\\
 &=\frac{2|Y|-r+a -r -a}{2|Y|-r+a}\\
 &=1-\frac{r+a }{2|Y|-r+a}\\
 &=1-f(r,a)\\
\end{split}
\end{equation}$$

The penalty factor $f(r,a)$ is null when $a=r=0$. We thus have $Dice=1$ as expected.

We can see that $f(a,r)\geq 0$.

Also, $\frac{\partial f}{\partial r}\gt 0$ and $\frac{\partial f}{\partial a}\geq 0$, show that small variations of $a$ or $r$ increase $f(a,r)$, and thus decrease the Dice coefficient, as expected.

