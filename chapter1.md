---
title: 'Probability Theory'
description: 'Chapter description goes here.'
---

## Sampling

```yaml
type: NormalExercise
key: 2bafef99a3
lang: r
xp: 100
skills: 1
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
ex() %>% check_function('integrate') %>% check_result() %>% check_equal()
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
