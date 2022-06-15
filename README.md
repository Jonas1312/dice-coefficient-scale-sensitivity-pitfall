# Dice Coefficient and Its Sensitivity to Scale

In computer vision, we often use the Dice score to quantify the quality of a generated segmentation to its ground truth: 

$$Dice = 2\frac{|Y\cap \hat{Y}|}{|Y| + |\hat{Y}|}$$

Where:
- $|Y|$ is the ground truth
- $|\hat{Y}|$ the estimate or prediction.

Let's name $r$ as the number of pixels removed by the estimate, that is the number of false negatives FN:

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

We can see that $f(r,a)\geq 0$.

Also $\frac{\partial f}{\partial r}\gt 0 $ and $\frac{\partial f}{\partial a}\geq 0$ show that small variations of $a$ or $r$ increase $f(r,a)$, and thus decrease the Dice coefficient, as expected.

However, the interesting thing is that $f(r,a)$ also depends on the size of the ground truth $|Y|$.

$f(r,a)$ decreases when the size $|Y| $ increases, which means that for two ground truth segmentations where $|Y_1|<|Y_2| $, and with the same number of pixel-wise errors $r+a$, we will have $Dice(Y_1, \hat{Y_1}) \lt Dice(Y_2, \hat{Y_2})$.

In other terms, it means that Dice overpenalises small objects, and is too tolerant with big objects.

Using a Dice loss or a Dice metric on a dataset with many different sizes of objects will cause your model to be biased.

A solution might be to use the [Generalized Dice Loss](https://arxiv.org/abs/1707.03237).
