---
layout: post
title: "R - Simulation"
date: 2019-02-21
description: ""
tags: CS R
redirect_from:
  - /posts/c3af451e/
---

## Learning Objectives

- Call the str function on an arbitrary R object
- Simulate a random normal variable with an arbitrary mean and standard deviation
- Simulate data from a normal linear model

## the str Function

str: compactly display the internal structure of an R object

```r
str(str)
```

```
function (object, ...)
```

```r
str(lm)
```

```
function (formula, data, subset, weights, na.action, method = "qr", model = TRUE, 
    x = FALSE, y = FALSE, qr = TRUE, singular.ok = TRUE, contrasts = NULL, 
    offset, ...)
```

```r
str(ls)
```

```
function (name, pos = -1L, envir = as.environment(pos), all.names = FALSE, 
    pattern, sorted = TRUE)
```

```r
x <- rnorm(100, 2, 4)
```

```r
summary(x)
```

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
 -6.721  -0.807   1.981   1.919   4.352  15.838
```

```r
str(x)
```

```
 num [1:100] 3.27 3.93 6.42 1.62 3.36 ...
```

```r
f <- gl(40, 10)
```

```r
str(f)
```

```
 Factor w/ 40 levels "1","2","3","4",..: 1 1 1 1 1 1 1 1 1 1 ...
```

```r
library(datasets)
```

```r
head(airquality)
```

| Ozone | Solar.R | Wind | Temp | Month | Day |
| --- | --- | --- | --- | --- | --- |
| 41 | 190 | 7.4 | 67 | 5 | 1 |
| 36 | 118 | 8.0 | 72 | 5 | 2 |
| 12 | 149 | 12.6 | 74 | 5 | 3 |
| 18 | 313 | 11.5 | 62 | 5 | 4 |
| NA | NA | 14.3 | 56 | 5 | 5 |
| 28 | NA | 14.9 | 66 | 5 | 6 |

```r
str(airquality)
```

```
'data.frame':    153 obs. of  6 variables:
 $ Ozone  : int  41 36 12 18 NA 28 23 19 8 NA ...
 $ Solar.R: int  190 118 149 313 NA NA 299 99 19 194 ...
 $ Wind   : num  7.4 8 12.6 11.5 14.3 14.9 8.6 13.8 20.1 8.6 ...
 $ Temp   : int  67 72 74 62 56 66 65 59 61 69 ...
 $ Month  : int  5 5 5 5 5 5 5 5 5 5 ...
 $ Day    : int  1 2 3 4 5 6 7 8 9 10 ...
```

```r
m <- matrix(rnorm(100), 10, 10)
```

```r
str(m)
```

```
 num [1:10, 1:10] 1.3157 -0.8322 -1.1879 1.0607 -0.0914 ...
```

```r
m[,1]
```

1. 1.31574855435227
2. -0.832218308577875
3. -1.18790192747972
4. 1.0606597056878
5. -0.0913834161339654
6. 0.25791756367502
7. -1.37134438815737
8. 0.313414400144491
9. 1.43525092704093
10. -0.373120195016343

```r
s <- split(airquality, airquality$Month)
```

```r
str(s)
```

```
List of 5
 $ 5:'data.frame':    31 obs. of  6 variables:
  ..$ Ozone  : int [1:31] 41 36 12 18 NA 28 23 19 8 NA ...
  ..$ Solar.R: int [1:31] 190 118 149 313 NA NA 299 99 19 194 ...
  ..$ Wind   : num [1:31] 7.4 8 12.6 11.5 14.3 14.9 8.6 13.8 20.1 8.6 ...
  ..$ Temp   : int [1:31] 67 72 74 62 56 66 65 59 61 69 ...
  ..$ Month  : int [1:31] 5 5 5 5 5 5 5 5 5 5 ...
  ..$ Day    : int [1:31] 1 2 3 4 5 6 7 8 9 10 ...
 $ 6:'data.frame':    30 obs. of  6 variables:
  ..$ Ozone  : int [1:30] NA NA NA NA NA NA 29 NA 71 39 ...
  ..$ Solar.R: int [1:30] 286 287 242 186 220 264 127 273 291 323 ...
  ..$ Wind   : num [1:30] 8.6 9.7 16.1 9.2 8.6 14.3 9.7 6.9 13.8 11.5 ...
  ..$ Temp   : int [1:30] 78 74 67 84 85 79 82 87 90 87 ...
  ..$ Month  : int [1:30] 6 6 6 6 6 6 6 6 6 6 ...
  ..$ Day    : int [1:30] 1 2 3 4 5 6 7 8 9 10 ...
 $ 7:'data.frame':    31 obs. of  6 variables:
  ..$ Ozone  : int [1:31] 135 49 32 NA 64 40 77 97 97 85 ...
  ..$ Solar.R: int [1:31] 269 248 236 101 175 314 276 267 272 175 ...
  ..$ Wind   : num [1:31] 4.1 9.2 9.2 10.9 4.6 10.9 5.1 6.3 5.7 7.4 ...
  ..$ Temp   : int [1:31] 84 85 81 84 83 83 88 92 92 89 ...
  ..$ Month  : int [1:31] 7 7 7 7 7 7 7 7 7 7 ...
  ..$ Day    : int [1:31] 1 2 3 4 5 6 7 8 9 10 ...
 $ 8:'data.frame':    31 obs. of  6 variables:
  ..$ Ozone  : int [1:31] 39 9 16 78 35 66 122 89 110 NA ...
  ..$ Solar.R: int [1:31] 83 24 77 NA NA NA 255 229 207 222 ...
  ..$ Wind   : num [1:31] 6.9 13.8 7.4 6.9 7.4 4.6 4 10.3 8 8.6 ...
  ..$ Temp   : int [1:31] 81 81 82 86 85 87 89 90 90 92 ...
  ..$ Month  : int [1:31] 8 8 8 8 8 8 8 8 8 8 ...
  ..$ Day    : int [1:31] 1 2 3 4 5 6 7 8 9 10 ...
 $ 9:'data.frame':    30 obs. of  6 variables:
  ..$ Ozone  : int [1:30] 96 78 73 91 47 32 20 23 21 24 ...
  ..$ Solar.R: int [1:30] 167 197 183 189 95 92 252 220 230 259 ...
  ..$ Wind   : num [1:30] 6.9 5.1 2.8 4.6 7.4 15.5 10.9 10.3 10.9 9.7 ...
  ..$ Temp   : int [1:30] 91 92 93 93 87 84 80 78 75 73 ...
  ..$ Month  : int [1:30] 9 9 9 9 9 9 9 9 9 9 ...
  ..$ Day    : int [1:30] 1 2 3 4 5 6 7 8 9 10 ...
```

## Simulation - Generating Random Numbers

- rnorm
- dnorm
- pnorm
- rpois

```r
str(rnorm)
```

```
function (n, mean = 0, sd = 1)
```

```r
str(dnorm)
```

```
function (x, mean = 0, sd = 1, log = FALSE)
```

```r
str(qnorm)
```

```
function (p, mean = 0, sd = 1, lower.tail = TRUE, log.p = FALSE)
```

```r
str(rpois)
```

```
function (n, lambda)
```

```r
x <- rnorm(10)
x
```

1. -0.666087369538605
2. -1.44040880956661
3. -1.48646639016783
4. -0.418159685775961
5. 0.58542380531235
6. -1.25321348722927
7. -1.27424584122045
8. 0.691700091609917
9. 0.174510667558016
10. 0.573314450069069

```r
x <- rnorm(10, 20, 2)
x
```

1. 17.9435304870445
2. 19.5724651543841
3. 19.2634280201875
4. 15.6159308600513
5. 21.5861218732645
6. 21.7677118003667
7. 18.3658321172365
8. 16.659817189802
9. 19.9214964631997
10. 19.3704904422907

```r
summary(x)
```

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
-1.4865 -1.2690 -0.5421 -0.4514  0.4736  0.6917
```

### Generating the same random number

```r
set.seed(1)
rnorm(5)
```

1. -0.626453810742332
2. 0.183643324222082
3. -0.835628612410047
4. 1.59528080213779
5. 0.329507771815361

```r
rnorm(5)
```

1. -0.820468384118015
2. 0.487429052428485
3. 0.738324705129217
4. 0.575781351653492
5. -0.305388387156356

```r
set.seed(1)
rnorm(5)
```

1. -0.626453810742332
2. 0.183643324222082
3. -0.835628612410047
4. 1.59528080213779
5. 0.329507771815361

```r
rpois(10, 1)
```

1. 0
2. 0
3. 1
4. 1
5. 2
6. 1
7. 1
8. 4
9. 1
10. 2

```r
rpois(10, 2)
```

1. 2
2. 3
3. 0
4. 4
5. 1
6. 3
7. 1
8. 1
9. 2
10. 4

```r
rpois(10, 20)
```

1. 23
2. 20
3. 11
4. 22
5. 24
6. 16
7. 17
8. 18
9. 17
10. 21

```r
ppois(2, 2)
```

0.676676416183063

```r
ppois(4, 2)
```

0.947346982656289

```r
ppois(6, 2)
```

0.995466194473751

## Simulation - Simulating a Linear Model

```r
set.seed(20)
x <- rnorm(100)
e <- rnorm(100, 0, 2)
y <- 0.5 + 2 * x + e
```

```r
summary(y)
```

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
-6.4084 -1.5402  0.6789  0.6893  2.9303  6.5052
```

```r
plot(x, y)
```

![png](/assets/img/output_41_0.png)

```r
set.seed(10)
x <- rbinom(100, 1, 0.5)
e <- rnorm(100, 0, 2)
y <- 0.5 + 2 * x + e
```

```r
summary(y)
```

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
-3.4936 -0.1409  1.5767  1.4322  2.8397  6.9410
```

```r
plot(x, y)
```

![png](/assets/img/output_44_0.png)

```r
set.seed(1)
x <- rnorm(100)
log.mu <- 0.5 + 0.3 * x
y <- rpois(100, exp(log.mu))
summary(y)
```

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    1.00    1.00    1.55    2.00    6.00
```

```r
plot(x, y)
```

![png](/assets/img/output_46_0.png)

## Simualtion - Rnadom Sampling

```r
set.seed(1)
sample(1:10, 4)
```

1. 3
2. 4
3. 5
4. 7

```r
sample(1:10, 4)
```

1. 3
2. 9
3. 8
4. 5

```r
sample(letters, 5)
```

1. 'q'
2. 'b'
3. 'e'
4. 'x'
5. 'p'

```r
sample(1:10)
```

1. 4
2. 7
3. 10
4. 6
5. 9
6. 2
7. 8
8. 3
9. 1
10. 5

```r
sample(1:10)
```

1. 2
2. 3
3. 4
4. 1
5. 9
6. 5
7. 10
8. 8
9. 6
10. 7

```r
sample(1:10, replace = TRUE)
```

1. 2
2. 9
3. 7
4. 8
5. 2
6. 8
7. 5
8. 9
9. 7
10. 8
