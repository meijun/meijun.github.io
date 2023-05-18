We often do some calculations in the log space to avoid the overflow of `float64`. The multiplication is the addition in the log space. The addition is the LogSumExp calculation in the log space. In the beginning, we want to calculate $\alpha \times \beta$ and $\alpha + \beta$. When we calculate them in the log space, let $a=log(\alpha)$, $b=log(\beta)$,

$$\begin{split}
log(\alpha \times \beta) &= a + b \\
log(\alpha + \beta) &= log(e^a + e^b) \\
&= log(sum(exp(a), exp(b))) \\
&=: LogSumExp(a, b)
\end{split}$$

However, when we calculate the addition $log(\alpha + \beta)$, if $a$ is more than $710$, then $exp(a)$ will be `+Inf` in `float64`, even the real final result is not so big. Assumed $a > b$, we can do the algebra:

$$\begin{split}
LogSumExp(a, b) &= log(e^a + e^b) \\
&= log(e^a (1 + e^{b-a})) \\
&= a + log(1 + e^{b-a})
\end{split}$$

That's why the calculation $log(1+x)$ is very important. Most of the languages give the function `Log1p(x)`, which can calculate $log(1+x)$ more accurately without the underflow. Here is my `LogSumExp` function in Go.

```go
import "math"

func LogSumExp(a, b float64) float64 {
	if a < b {
		a, b = b, a
	}
	if math.IsInf(a, 0) {
		return a
	}
	return a + math.Log1p(math.Exp(b - a))
}
```
