---
author: teymur
comments: true
date: 2018-03-06 22:16:08+00:00
layout: post
slug: arithmetic-series
title: Arithmetic Series
categories: Tutorial
tags:
- math
---

## Arithmetic series
```
a = {1,2,3,4,5,6,...,n}

sum1 = 1+2+3+4 ... n
sum2 = n + (n-1) + (n-2) + (n-3) ..   

sum1+sum2 = (n+1) + (n+1) + (n+1) + (n+1) ...

2sum = n(n+1);
sum = n(n+1)/2

n - last 
1 - first

```

### Arithmetic sequences

```
seq = {1,5,9,13..}

f(n) = 1 + 4(n-1)

sum of seq 
d = 4
a = 1

sum1  = a + (a + d) + (a + 2d) + (a + 3d) + ... + (a + (n-1)d)
sum2  = (a + (n-1)d) + (a + (n-2)d) + (a + (n-3)d) + .. (a + (n - z)d)
sum3  = sum1 + sum2 = a + (a + (n-1)d) + (a + d) + (a + (n-2)d) .... 
sum3  = 2a + (n-1)d + 2a + (n-1)d.... = n(2a+(n-1)d)

sum = (2a+(n-1)d)/2

n( a +  a + (n-1)d) / 2 
first half a/2  + last haft (a + (n-1)d)/2 multiply n times
```
Example 1
```
11+20+29+...+4052
```

Solution 1 
```
d = 9
a = 11
11 + 9(n-1) = 4052
9n = 4050
n = 450
```
Solution 2
```
(4052-11)/9=449

from 11 to reach 4052 you nead 499 steps 
add first step 450 steps

```
The sum of a series
```
sum = (2a+(n-1)d)/2

((2x11 + (550-1)x9/2) x 450

((11+4052)/2)x450
```

Example 2 
```
10+(−1)+(−12)+...+(−10,979)=
10-11(n-1) = - 10979

n = 1000

((10 +(-10979))/2)x1000  = -5484500
```

Example 3
```
k=1
∑ (−5k+12)= ?
275
​	 
−5k+12=7      k=1
−5k+12=-1363  k=275

sum = ((-1363+7)/2)x275 = -186450
```

## Geometric series
```
a = first term
r =  common ratio
n = # of terms
Sn = sum of n terms

Sn = a + ar + ar^2 + ... ar^n-1
-rSn = -ra - ar^2 - ... - ar^n

Sn  - rSn = a - ar^n
Sn(1-r) = a - ar^n

Sn  = (a-ar^n )/1-r 
```