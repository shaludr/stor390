Programming in R
========================================================
author: STOR 390
date: 1/26/17
autosize: true

This lecture is about
========================================================
- conditionals (if/else)
- loops (for, while)
- bow to define your own functions
- basic programming flow




References
========================================================
- section 19 ([functions](http://r4ds.had.co.nz/functions.html)
- 21.1-21.3



if statements
========================================================

```r
if (2 > 1) {
  print('fact')
}
```

```
[1] "fact"
```




if statements
========================================================


```r
if (2 < 1) {
  print('alternative fact')
}
```



if/else statements
========================================================

```r
# Flip a coin 
if (runif(1) < 0.5) {
    print('heads')
} else {
    print('tails')
}
```

```
[1] "tails"
```


else-if statements
========================================================

```r
r <- runif(1)
# rock paper sissors
if (r < 1/3) {
    print('rock')
} else if (1/3 < r && r < 2/3) {
    print('paper')
} else{
    print('scissors')
}
```

```
[1] "rock"
```


Equality
========================================================

```r
2*5 == 10
```

```
[1] TRUE
```


Beware of finite precision arithmetic
========================================================

```r
# oops
sqrt(2)^2 == 2
```

```
[1] FALSE
```

Safety first
========================================================

```r
dplyr::near(sqrt(2)^2, 2)
```

```
[1] TRUE
```

Vectorized operations
========================================================

```r
c(1, 1, 1) == c(1, 2, 1)
```

```
[1]  TRUE FALSE  TRUE
```

Use the double symbol in for loops
========================================================

default to `&&` or `||` in a for loop

```r
c(T, T, T) || c(T, F, T)
```

```
[1] TRUE
```


Otherwise you get a vector
========================================================

```r
c(T, T, T) | c(T, F, T)
```

```
[1] TRUE TRUE TRUE
```

Loops
========================================================
- for
- while


for loops
========================================================

```r
for (i in 1:10) {
  print(i)
}
```

```
[1] 1
[1] 2
[1] 3
[1] 4
[1] 5
[1] 6
[1] 7
[1] 8
[1] 9
[1] 10
```


Pre-allocate memory 
========================================================

```r
nums <- vector("double", 10) # or rep(0, 10) or something else
for (i in 1:10) {
  nums[i] <- runif(1)
}
```

Dynamic allocation bad
========================================================

```r
# nums <- c()
# for (i in 1:10) {
#   nums <- c(nums, runif(1))
# }
```


while loops
========================================================

```r
current_position <- 10
n_iter <- 0
while (current_position > 0){
    current_position <- current_position + rnorm(1)
    n_iter <- n_iter + 1
}
print(paste0('you lost all your money after ', n_iter, ' trips to the casino'))
```

```
[1] "you lost all your money after 103 trips to the casino"
```


Infinite loops
========================================================

```r
while (TRUE){
    print('Duke sucks')
}
```

Vectorization
========================================================
Try to vectorize anything you can (once you learn what that means...)

```r
sapply(1:10, function(x) x * 2)
```

Functions are for humans and computers
========================================================
- break long program up into small chunks
- more readable
- code reuse
    - catch errors
    - don't have to copy/paste
- only need to fix code in one place

When to write a function?
========================================================
> You should consider writing a function whenever you’ve copied and pasted a block of code more than twice

Define a function
========================================================

```r
power <- function(num, exponent){
    # returns num raised to the exponent
    num ^ exponent
}

power(2, 3)
```

```
[1] 8
```

Default arguments
========================================================

```r
power <- function(num, exponent=3){
    # returns num raised to the exponent
    num ^ exponent
}

power(2)
```

```
[1] 8
```

Return values
========================================================

```r
random_rps <- function(){
    # randomly returns one of rock, paper or scissors
    
    r <- runif(1)
    # rock paper sissors
    if (r < 1/3) {
        return('rock')
    } else if (1/3 < r && r < 2/3) {
        return('paper')
    } else{
        return('scissors')
    }
}

random_rps()
```

```
[1] "scissors"
```

Write functions in separate scripts and import them
========================================================

```r
source('fun.R')

helper_fun()
```

```
[1] "Im not a very helpful helper function"
```

Michael Jordan
========================================================
**I basically know of two principles for treating complicated systems in
simple ways; the first is the principle of modularity and the second is the
principle of abstraction.** I am an apologist for computational probability
in machine learning, and particularly for graphical models and variational
methods, because I believe that probability theory implements these two
principles in deep and intriguing ways – namely through factorization and
through averaging. Exploiting these two mechanisms as fully as possible
seems to me to be the way forward in machine learning.

Michael I. Jordan Massachusetts Institute of Technology, 1997.

(quote borrowed from Ben Vigoda's thesis)

Modularity and abstraction
========================================================
- modularity
    - break a complicated task into many smaller sub-tasks
- abstraction
    - you don't need to  know the inner workings of every part of the system, just how things interact

More topics
========================================================
- testing
- vectorization
- recursion
- debugging / profiling
- environments / scoping
- object oriented programming
- functional programming
- non-standard evaluation
- dynamic programming
- memory usage
- using Rcpp


Lab 3
========================================================
See [https://idc9.github.io/stor390/labs/3/prog_lab.html](https://idc9.github.io/stor390/labs/3/prog_lab.html) for lab 3