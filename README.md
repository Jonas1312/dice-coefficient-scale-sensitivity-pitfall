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
\end{split}
\end{equation}$$
