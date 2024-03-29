---
title: Probability Theory
description: Chapter description goes here.
---

## Sampling

```yaml
type: NormalExercise
key: 2bafef99a3
lang: r
xp: 100
skills:
  - 1
```

Suppose you are the lottery fairy in a weekly lottery, where $6$ out of $49$ *unique* numbers are drawn.

`@instructions`
+ Draw the winning numbers for this week.

`@hint`
+ You may use the function <tt>sample()</tt> to draw random numbers, see <tt>?sample</tt>.
+ The set of elements to be sampled from here is $\\{1,...,49\\}$.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# draw the winning numbers for this week


```

`@solution`
```{r}
# draw the winning numbers for this week
sample(1:49, size = 6)

```

`@sct`
```{r}
ex() %>% check_function("sample") %>% {
  check_arg(., "x") %>% check_equal()
  check_arg(., "size") %>% check_equal()
}
success_msg("Well done!")
```

---

## Probability Density Function

```yaml
type: NormalExercise
key: 5d152aaf19
xp: 100
```

Consider a random variable $X$ with probability density function (PDF)

$$f_X(x)=\\frac{x}{4}e^{-x^2/8},\\quad x\\geq 0.$$

`@instructions`
+ Define the PDF from above as a function <tt>f()</tt>. <tt>exp(a)</tt> computes $e^a$.
+ Check whether the function you have defined is indeed a PDF.

`@hint`
+ Use <tt>function(x) {...}</tt> to define a function which takes the argument <tt>x</tt>.
+ In order for <tt>f()</tt> to be a PDF, its integral over the whole domain has to equal 1: $\\int_0^\\infty f\_X(x)\\mathrm{d}x=1$.
+ The function <tt>integrate()</tt> performs integration. You have to specify the function to be integrated as well as lower and upper limits of integration. These may be set to $[0,\\infty]$ by setting the corresponding arguments to <tt>0</tt> and <tt>Inf</tt>. You can access the numerical value of the computed integral by appending <tt>$value</tt>. See <tt>?integral</tt> for a detailed description of the function.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# define the PDF

   
# integrate f over the domain


```

`@solution`
```{r}
# define the PDF
f <- function(x){x/4*exp(-x^2/8)}
   
# integrate f over the domain
integrate(f, 0, Inf)$value

```

`@sct`
```{r}
ex() %>% check_fun_def("f") %>% {
  check_arguments(.)
  check_call(., 1) %>% check_result() %>% check_equal()
  check_call(., 4) %>% check_result() %>% check_equal()
  check_call(., 10) %>% check_result() %>% check_equal()
  check_call(., 100) %>% check_result() %>% check_equal()
  check_body(.) %>% check_function(., "exp")
}
ex() %>% check_function("integrate") %>% {
  check_arg(., "f") %>% check_equal(eval = FALSE)
  check_arg(., "lower") %>% check_equal()
  check_arg(., "upper") %>% check_equal()
}
success_msg("Great work!")
```

---

## Expected Value and Variance

```yaml
type: NormalExercise
key: 457fe23524
xp: 100
```

In this exercise you have to compute the expected value and the variance of the random variable $X$ considered in the previous exercise.

The PDF <tt>f()</tt> from the previous exercise is available in your working environment.

`@instructions`
+ Define a suitable function <tt>ex()</tt> which integrates to the expected value of $X$.
+ Compute the expected value of $X$. Store the result in <tt>expected_value</tt>.
+ Define a suitable function <tt>ex2()</tt> which integrates to the expected value of $X^2$.
+ Compute the variance of $X$. Store the result in <tt>variance</tt>.

`@hint`
+ The expected value of $X$ is defined as $E(X)=\\int_0^\\infty xf\_X(x)\\mathrm{d}x$.
+ The value of an integral computed by <tt>integrate()</tt> can be obtained via <tt>$value</tt>.
+ The variance of $X$ is defined as $Var(X)=E(X^2)-E(X)^2$, where $E(X^2)=\\int_0^\\infty x^2f\_X(x)\\mathrm{d}x$.

`@pre_exercise_code`
```{r}
f <- function(x){(x/4)*exp(-x^2/8)}
```

`@sample_code`
```{r}
# define the function ex


# compute the expected value of X


# define the function ex2


# compute the variance of X


```

`@solution`
```{r}
# define the function ex
ex <- function(x){x*f(x)}

# compute the expected value of X
expected_value <- integrate(ex, 0, Inf)$value

# define the function ex2
ex2 <- function(x){x^2*f(x)}

# compute the variance of X
variance <- integrate(ex2, 0, Inf)$value - expected_value^2

```

`@sct`
```{r}
ex() %>% check_fun_def("ex") %>% {
  check_arguments(.)
  check_call(., 1) %>% check_result() %>% check_equal()
  check_call(., 4) %>% check_result() %>% check_equal()
  check_call(., 10) %>% check_result() %>% check_equal()
  check_call(., 100) %>% check_result() %>% check_equal()
  check_body(.) %>% check_function(., "f")
}
ex() %>% check_function("integrate", index = 1) %>% {
  check_arg(., "f") %>% check_equal(eval = FALSE)
  check_arg(., "lower") %>% check_equal()
  check_arg(., "upper") %>% check_equal()
}
ex() %>% check_object("expected_value") %>% check_equal()
ex() %>% check_fun_def("ex2") %>% {
  check_arguments(.)
  check_call(., 1) %>% check_result() %>% check_equal()
  check_call(., 4) %>% check_result() %>% check_equal()
  check_call(., 10) %>% check_result() %>% check_equal()
  check_call(., 100) %>% check_result() %>% check_equal()
  check_body(.) %>% check_function(., "f")
}
ex() %>% check_function("integrate", index = 2) %>% {
  check_arg(., "f") %>% check_equal(eval = FALSE)
  check_arg(., "lower") %>% check_equal()
  check_arg(., "upper") %>% check_equal()
}
ex() %>% check_object("variance") %>% check_equal()
success_msg("Good job!")
```

---

## Standard Normal Distribution I

```yaml
type: NormalExercise
key: f0622e59c7
xp: 100
```

Let $Z\\sim\\mathcal{N}(0, 1)$.

`@instructions`
+ Compute $\\phi(3)$, that is, the value of the standard normal density at $c=3$.

`@hint`
+ Values of $\\phi(\\cdot)$ can be computed using <tt>dnorm()</tt>. Note that by default <tt>dnorm()</tt> uses <tt>mean = 0</tt> and <tt>sd = 1</tt>, so there is no need to set the corresponding arguments when you wish to obtain density values of the standard normal distribution.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# compute the value of the standard normal density at c=3


```

`@solution`
```{r}
# compute the value of the standard normal density at c=3
dnorm(3)

```

`@sct`
```{r}
ex() %>% check_function("dnorm") %>% check_result() %>% check_equal()
success_msg("Well done!")
```

---

## Standard Normal Distribution II

```yaml
type: NormalExercise
key: eb56223310
xp: 100
```

Let $Z\\sim\\mathcal{N}(0, 1)$.

`@instructions`
+ Compute $P(|Z|\\leq 1.64)$ by using the function <tt>pnorm()</tt>.

`@hint`
+ $P(|Z|\\leq z) = P(-z \\leq Z \\leq z)$.
+ Probabilities of the form $P(a \\leq Z \\leq b)$ can be computed as $P(Z\\leq b)-P(Z\\leq a)=F\_Z(b)-F\_Z(a)$ with $F\_Z(\\cdot)$ the cumulative distribution function (CDF) of $Z$. Alternatively, you may exploit the symmetry of the standard normal distribution.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# compute the probability


```

`@solution`
```{r}
# compute the probability
pnorm(1.64) - pnorm(-1.64)

```

`@sct`
```{r}
ex() %>% check_or(
  check_function(., "pnorm"),
  check_code(., "dnorm", fixed = T)
)
ex() %>% check_output_expr("1 - 2*pnorm(-1.64)")
success_msg("Good Job!")
```

---

## Normal Distribution I

```yaml
type: NormalExercise
key: fc7b7c446b
xp: 100
```

Let $Y\\sim\\mathcal{N}(5, 25)$.

`@instructions`
+ Compute the 99% quantile of the given distribution, i.e., find $y$ such that $\\Phi\\left(\\frac{y-5}{5}\\right)=0.99$.

`@hint`
+ You can compute quantiles of the normal distribution by using the function <tt>qnorm()</tt>.
+ Besides the quantile to be computed you have to specify the mean and the standard deviation of the distribution. This is done via the arguments <tt>mean</tt> and <tt>sd</tt>. Note that <tt>sd</tt> sets the standard deviation, not the variance!
+ <tt>sqrt(a)</tt> returns the square root of the numeric argument <tt>a</tt>.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# compute the 99% quantile of a normal distribution with mu = 5 and sigma^2 = 25.


```

`@solution`
```{r}
# compute the 99% quantile of a normal distribution with mu = 5 and sigma^2 = 25.
qnorm(0.99, mean = 5, sd = sqrt(25))

```

`@sct`
```{r}
ex() %>% check_function("qnorm") %>% check_result() %>% check_equal()
success_msg("Great work!")
```

---

## Normal Distribution II

```yaml
type: NormalExercise
key: e13d86de1c
xp: 100
```

Let $Y\\sim\\mathcal{N}(2, 12)$.

`@instructions`
+ Generate $10$ random numbers from this distribution.

`@hint`
+ You can use <tt>rnorm()</tt> to draw random numbers from a normal distribution.
+ Besides the number of draws you have to specify the mean and the standard deviation of the distribution. This can be done via the arguments <tt>mean</tt> and <tt>sd</tt>. Note that <tt>sd</tt> requires the standard deviation, not the variance!

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# generate 10 random numbers from the given distribution.


```

`@solution`
```{r}
# generate 10 random numbers from the given distribution.
rnorm(10, mean = 2, sd = sqrt(12))

```

`@sct`
```{r}
ex() %>% check_function("rnorm") %>% {
  check_arg(., "n") %>% check_equal()
  check_arg(., "mean") %>% check_equal()
  check_arg(., "sd") %>% check_equal()
}
success_msg("Great work!")
```

---

## Chi-squared Distribution I

```yaml
type: NormalExercise
key: 7c6da7fa91
xp: 100
```

Let $W\\sim\\chi^2\_{10}$.

`@instructions`
+ Plot the corresponding PDF using <tt>curve()</tt>. Specify the range of x-values as $[0,25]$ via the argument <tt>xlim</tt>.

`@hint`
+ <tt>curve()</tt> expects a function and its parameters as arguments (here <tt>dchisq()</tt> and the degrees of freedom <tt>df</tt>).
+ The range of x-values in <tt>xlim</tt> can be passed as a vector of interval bounds.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# plot the PDF of a chi^2 random variable with df = 10


```

`@solution`
```{r}
# plot the PDF of a chi^2 random variable with df = 10
curve(dchisq(x, df = 10), xlim = c(0, 25))

```

`@sct`
```{r}
ex() %>% check_function("curve") %>% {
  check_arg(., "expr") # does not work
  check_arg(., "xlim") %>% check_equal()
}
# more robust SCT needed
ex() %>% check_code("dchisq", fixed = T)
success_msg("Great work!")
```

---

## Chi-squared Distribution II

```yaml
type: NormalExercise
key: 8e4a8cc2ef
xp: 100
```

Let $X\_1$ and $X\_2$ be two independent normally distributed random variables with $\\mu=0$ and $\\sigma^2=15$.

`@instructions`
+ Compute $P(X\_1^2+X\_2^2>10)$.

`@hint`
+ Note that $X\_1$ and $X\_2$ are not $\\mathcal{N}(0,1)$ but $\\mathcal{N}(0,15)$ distributed. Hence you have to scale appropriately. Afterwards you can use <tt>pchisq()</tt> to compute the probability.
+ The argument <tt>lower.tail</tt> may be helpful.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# compute the probability


```

`@solution`
```{r}
# compute the probability
pchisq(10/15, df = 2, lower.tail = F)

```

`@sct`
```{r}
ex() %>% check_or(
  check_function(., "pchisq"),
  check_code(., "dchisq", fixed = T)
)
ex() %>% check_output_expr("1 - pchisq(10/15, df = 2)")
success_msg("Great work!")
```

---

## Student t Distribution I

```yaml
type: NormalExercise
key: e0e653696b
xp: 100
```

Let $X\\sim t\_{10000}$ and $Z\\sim\\mathcal{N}(0,1)$.

`@instructions`
+ Compute the $95\\%$ quantile of both distributions. What do you notice?

`@hint`
+ You may use <tt>qt()</tt> and <tt>qnorm()</tt> to compute quantiles of the given distributions.
+ For the $t$ distribution you have to specify the degrees of freedom <tt>df</tt>.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# compute the 95% quantile of a t distribution with 10000 degrees of freedom


# compute the 95% quantile of a standard normal distribution


```

`@solution`
```{r}
# compute the 95% quantile of a t distribution with 10000 degrees of freedom
qt(0.95, df = 10000)

# compute the 95% quantile of a standard normal distribution
qnorm(0.95)

```

`@sct`
```{r}
ex() %>% check_function("qt") %>% check_result() %>% check_equal()
ex() %>% check_function("qnorm") %>% check_result() %>% check_equal()
success_msg("Correct! A t-distributed RV converges to a standard normal as the degrees of freedom get large.")
```

---

## Student t Distribution II

```yaml
type: NormalExercise
key: 141baf52d5
xp: 100
```

Let $X\\sim t\_1$. 

Once the session has initialized you will see the plot of the corresponding probability density function (PDF).

`@instructions`
+ Generate $1000$ random numbers from this distribution and assign them to the variable <tt>x</tt>.
+ Compute the sample mean of <tt>x</tt>. Can you explain the result?

`@hint`
+ You can use <tt>rt()</tt> to draw random numbers from a t distribution.
+ Note that the t distribution is fully determined through the degree(s) of freedom. Specify them via the argument <tt>df</tt>.
+ To compute the sample mean of a vector you can use the function <tt>mean()</tt>.

`@pre_exercise_code`
```{r}
custom_seed(1)
```

`@sample_code`
```{r}
# generate 1000 random numbers from the given distribution. Assign them to the variable x.


# compute the sample mean of x.


```

`@solution`
```{r}
# generate 1000 random numbers from the given distribution. Assign them to the variable x.
x <- rt(1000, df = 1)

# compute the sample mean of x.
mean(x)

```

`@sct`
```{r}
ex() %>% check_object("x") %>% check_equal()
# allow for rcauchy()
ex() %>% check_function("mean") %>% check_result() %>% check_equal()
success_msg("Well done! The expectation is not defined for a t distributed RV with one degree of freedom: although a t distribution with M = 1 is, as every other t distribution, symmetric around zero it actually has no expectation. This explains the value of the sample mean not being close to zero.")
```

---

## F Distribution I

```yaml
type: NormalExercise
key: e4bfce6847
xp: 100
```

Let $Y\\sim F(10, 4)$.

`@instructions`
+ Plot the quantile function of the given distribution using the function <tt>curve()</tt>.

`@hint`
+ <tt>curve()</tt> expects the function with their respective parameters (here: degrees of freedom <tt>df1</tt> and <tt>df2</tt>) as an argument.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# plot the quantile function of the given distribution


```

`@solution`
```{r}
# plot the quantile function of the given distribution
curve(qf(x, df1 = 10, df2 = 4))

```

`@sct`
```{r}
ex() %>% check_function("curve") %>% check_arg(., "expr") # does not work, more robust SCT needed
ex() %>% check_code("qf", fixed = T)
success_msg("Well done!")
```

---

## F Distribution II

```yaml
type: NormalExercise
key: bfe9c95c43
xp: 100
```

Let $Y\\sim F(4,5)$.

`@instructions`
+ Compute $P(1<Y<10)$ by integration of the PDF.

`@hint`
+ Besides providing the function to be integrated, you have to specify lower and upper bounds of integration.
+ The additional parameters of the distribution (here <tt>df1</tt> and <tt>df2</tt>) also have to be passed *inside* the call of <tt>integrate()</tt>.
+ The value of the integral can be obtained via <tt>$value</tt>.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# compute the probability by integration


```

`@solution`
```{r}
# compute the probability by integration
integrate(df, lower = 1, upper = 10, df1 = 4, df2 = 5)$value

```

`@sct`
```{r}
ex() %>% check_function("integrate") %>% {
  check_arg(., "f") %>% check_equal(eval = FALSE)
  check_arg(., "lower") %>% check_equal()
  check_arg(., "upper") %>% check_equal()
  check_arg(., "df1") %>% check_equal()
  check_arg(., "df2") %>% check_equal()
}
success_msg("Great work!")
```
