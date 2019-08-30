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
ex() %>% check_or(
  check_function(., 'integrate') %>% check_result() %>% check_equal(),
  override_solution(., 'integrate(f, 0, Inf)') %>%
    check_function('integrate') %>% check_result() %>% check_equal()
)
success_msg("Great work!")
```
