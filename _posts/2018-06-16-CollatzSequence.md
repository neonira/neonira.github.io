---
layout: post
title: R - Math - Collatz sequence part V
category: category-rmetaverse
summary: overview and discovery of the Collatz sequence
image: images/maths/collatz/cs.png
# comments: true
permalink: rm-r-math-5
---

Find previous posts if you haven't yet read them. [first post](https://neonira.github.io/rm-r-math-1), [second post](https://neonira.github.io/rm-r-math-2), [third post](https://neonira.github.io/rm-r-math-3), and [fourth post](https://neonira.github.io/rm-r-math-4).   

## Numerical approach for number made of 1 unique digit

<span class='do'>
**First important result**  
All the numbers from 1 to 9, provides 1 as final output of Collatz sequence. This could be easily demonstrated numericaly, just by applying Collatz rule in sequence for each number. 
</span>

## Reverse analysis

Instead of starting from any number and applying Collatz sequence, let's do the exact opposite. I'll start from number 1, and will find its antecedents, and apply same logic on those ones.  

#### Case of number 1

1 is an odd number. Therefore it can only result from a division by two, applying <cite class='kw'>&eta;</cite> <cite class='refeq'>a</cite>.  
So its unique antecedent is 2.

#### Case of number 2

2 is an even number. Therefore it can only result from two distinct sources, applying <cite class='kw'>&omega;</cite> or <cite class='kw'>&eta;</cite> <cite class='refeq'>b</cite>.  
But <cite class='kw'>&omega;</cite> is not applicable as 3 * odd number + 1 is <cite class='math_ge'></cite> 4 in <cite class='math_N'></cite><sup>*</sup>.  
Therefore only antecedent of 2 is to be given by <cite class='kw'>&eta;</cite>, which gives 4. 

#### Case of number 4

<cite class='kw'>4</cite> is an even number. So <cite class='refeq'>b</cite> applies.  
Applying <cite class='kw'>&omega;</cite> gives <cite class='kw'>1</cite>.  
Applying <cite class='kw'>&eta;</cite> gives <cite class='kw'>8</cite>.  
We have two antecedents, but the first one is also the stopping condition, that has already been studied. 

#### Case of number 8
<cite class='kw'>8</cite> is an even number. So <cite class='refeq'>b</cite> applies.  
Applying <cite class='kw'>&omega;</cite> gives a result that is not in <cite class='math_N'></cite>. &nbsp;&nbsp; &nbsp; (8 - 1) / 3 = 7 / 3 <cite class='math_notin'></cite><cite class='math_N'></cite>.  
Applying <cite class='kw'>&eta;</cite> gives <cite class='kw'>16</cite>.  
We have one antecedent, that is <cite class='kw'>16</cite>.

#### <cite class='kw'>&omega;</cite> analysis

What are the conditions for <cite class='kw'>&omega;</cite> to bring a result in <cite class='math_N'></cite>, considering an input in <cite class='math_N'></cite>?  

<cite class='kw'> &omega;<sub>n + 1</sub></cite> = 3 <cite class='kw'> &omega;<sub>n</sub></cite> + 1 &nbsp;&nbsp;&nbsp; by definition

<cite class='kw'>&omega;<sub>n</sub></cite> = (<cite class='kw'> &omega;<sub>n+1</sub></cite> - 1) / 3   

Therefore a condition to find an antecedent of a number <cite class='kw'>p</cite> by <cite class='kw'>&omega;</cite> is that <cite class='kw'>p</cite> - 1 is multiple of 3.  


Given that p is a power of 2, following logic expressed previously in this post, then the only possibility for <cite class='kw'> &omega;<sub>n + 1</sub></cite> to be dividable by 3, it to be of the form 2<sup>2(q + 1)</sup> with <cite class='kw'>q</cite> &isin; <cite class='math_N'></cite>. Thus the condition that the exponent of 2 being even is sufficient.  

<cite class='kw'>&omega;<sub>n</sub></cite> = (<cite class='kw'> &omega;<sub>n+1</sub></cite> - 1) / 3 = (2<sup>2(q + 1)</sup>- 1) / 3


```r
> z <- 0:20
> omega <- 2^z
> omega
 [1]       1       2       4       8      16      32      64     128     256 
 [10]	 512    1024    2048    4096    8192   16384   32768   65536	131072
 [19] 262144  524288 1048576
> previous <- (omega - 1) / 3
> previous
 [1]  0.000000e+00 3.333333e-01 1.000000e+00 2.333333e+00 5.000000e+00 1.033333e+01
 [7]  2.100000e+01 4.233333e+01 8.500000e+01 1.703333e+02 3.410000e+02 6.823333e+02 
 [13] 1.365000e+03 2.730333e+03 5.461000e+03 1.092233e+04 2.184500e+04 4.369033e+04 
 [19] 8.738100e+04 1.747623e+05 3.495250e+05
> p <- which(previous %% 1 == 0)
> p
 [1]  1  3  5  7  9 11 13 15 17 19 21
> z[p]
 [1]  0  2  4  6  8 10 12 14 16 18 20
```

<span class='do'>
**Second important result**  
There is one and only one suite of numbers in Collatz sequence, that leads to stopping condition <cite class='comment'>i.e. reaching <cite class='kw'>1</cite></cite>that is the suite 2<sup>n</sup>, 2<sup>n-1</sup>, 2<sup>n-2</sup>, ..., 2<sup>2</sup>, 2<sup>1</sup>, 2<sup>0</sup>
</span>


The typical converging sequence if then finished by number suite: <cite class='kw'>16, 8, 4, 2, 1</cite>. It is important to note here, that <cite class='kw'>16</cite> ends with 6 and belongs to cluster 1, that <cite class='kw'>8</cite> ends with 8 and belongs to cluster 2, whereas all the remaining numbers of this suite, belong to cluster 3. Refer to previous posts, if you need.  

<span class='warn'>
**Corollary**  
If a Collatz sequence generated or stating number is a power of 2, then convergence to 1 is proven.
</span>


## Convergence analysis
I will now show, that whatever the number considered, Collatz sequence converges. To do so, I will partition <cite class='math_N'></cite>. 


Given following definitions  
P<sub>1</sub> = { n = 2p / n < 10}  
P<sub>2</sub> = { n = 2p / n <cite class='math_ge'></cite>10, p = 2 + 3k  k &isin; <cite class='math_N'></cite><sup>*</sup>}  
P<sub>3</sub> = { n = 2p / n <cite class='math_ge'></cite>10, p = 3 + 3k  k &isin; <cite class='math_N'></cite><sup>*</sup>}  
P<sub>4</sub> = { n = 2p / n <cite class='math_ge'></cite>10, p = 4 + 3k  k &isin; <cite class='math_N'></cite><sup>*</sup>}  
P = P<sub>1</sub> <cite class='math_union'></cite> P<sub>2</sub> <cite class='math_union'></cite>  P<sub>3</sub> <cite class='math_union'></cite>  P<sub>4</sub>  

So P is a partition of all even numbers from <cite class='math_N'></cite>. 
```r
> k <- 1:20
> p2 <- 2 * (2 + 3 * k)
> p3 <- 2 * (3 + 3 * k)
> p4 <- 2 * (4 + 3 * k)
> p2
 [1]  10  16  22  28  34  40  46  52  58  64  70  76  82  88  94 100 106 112 118 124
> p3
 [1]  12  18  24  30  36  42  48  54  60  66  72  78  84  90  96 102 108 114 120 126
> p4
 [1]  14  20  26  32  38  44  50  56  62  68  74  80  86  92  98 104 110 116 122 128
```


Numbers in P<sub>2</sub> are given by suite <cite class='kw'>&rho;</cite><sub>2,k</sub> = 6<cite class='kw'>k</cite> + 4 with <cite class='kw'>k</cite> &isin; <cite class='math_N'></cite><sup>*</sup>.

Numbers in P<sub>3</sub> are given by suite <cite class='kw'>&rho;</cite><sub>3,k</sub> = 6<cite class='kw'>k</cite> + 6 with <cite class='kw'>k</cite> &isin; <cite class='math_N'></cite><sup>*</sup>..  

Numbers in P<sub>4</sub> are given by suite <cite class='kw'>&rho;</cite><sub>4,k</sub> = 6<cite class='kw'>k</cite> + 8 with <cite class='kw'>k</cite> &isin; <cite class='math_N'></cite><sup>*</sup>.  

Since all are these numbers are even, then let's apply <cite class='kw'>&eta;</cite> to them.  

<cite class='kw'>&eta;</cite><sub>2,k</sub>(P<sub>2</sub>) = 3<cite class='kw'>k</cite> + 2 with <cite class='kw'>k</cite> &isin; <cite class='math_N'></cite><sup>*</sup>, which is even when <cite class='kw'>k</cite> is even, and odd when <cite class='kw'>k</cite> is odd.  

<cite class='kw'>&eta;</cite><sub>3,k</sub>(P<sub>3</sub>) = 3<cite class='kw'>k</cite> + 4 with <cite class='kw'>k</cite> &isin; <cite class='math_N'></cite><sup>*</sup>, which is even when <cite class='kw'>k</cite> is even, and odd when <cite class='kw'>k</cite> is odd.  

<cite class='kw'>&eta;</cite><sub>4,k</sub>(P<sub>4</sub>) = 3<cite class='kw'>k</cite> + 8 with <cite class='kw'>k</cite> &isin; <cite class='math_N'></cite><sup>*</sup>, which is even when <cite class='kw'>k</cite> is even, and odd when <cite class='kw'>k</cite> is odd.  


### Which partitions hold numbers that are power of 2

P<sub>2</sub> = 6<cite class='kw'>k</cite> + 4 = 2 (3<cite class='kw'>k</cite> + 2) = 2<sup>n</sup> with <cite class='kw'>k</cite> and <cite class='kw'>n</cite> &isin; <cite class='math_N'></cite><sup>*</sup>. Solution is the suite [<cite class='kw'>OEIS&#174; A020988</cite>](https://oeis.org/A020988) defined by <cite class='kw'>k</cite><sub>p</sub> = (2 / 3) * 4<sup>p-1</sup> with <cite class='kw'>p</cite> <cite class='math_gt'></cite> 3.  

Practicing this suite, it is easy to find <cite class='kw'>k</cite> for a given <cite class='kw'>n</cite>. Just compute numerically function (2<sup>n</sup> - 4) / 6 for even values of <cite class='kw'>n</cite>, starting from <cite class='kw'>4</cite>.

```r
> f <- function(n) (2^n - 4) / 6
> k <- f(2 * 2:12)
> k
 [1]       2      10      42     170     682    2730   10922   43690  174762
[10]  699050 2796202
> p2 <- 2 * (3 * k + 2)
> p2
 [1]       16       64      256     1024     4096    16384    65536   262144
 [9]  1048576  4194304 16777216
> n <- log(p2) / log(2)
> n
 [1]  4  6  8 10 12 14 16 18 20 22 24
```


P<sub>4</sub> = 6<cite class='kw'>k</cite> + 8 = 2 (3<cite class='kw'>k</cite> + 4) = 2<sup>n</sup> with <cite class='kw'>k</cite> and <cite class='kw'>n</cite> &isin; <cite class='math_N'></cite><sup>*</sup>.  

Practicing this suite, it is easy to find <cite class='kw'>k</cite> for a given <cite class='kw'>n</cite>. Just compute numerically function (2<sup>n</sup> - 8) / 6 for odd values of <cite class='kw'>n</cite>, starting from <cite class='kw'>5</cite>.

```r
> g <- function(n) (2^n - 8) / 6
> k <- g(2 * 2:12 + 1)
> k
 [1]       4      20      84     340    1364    5460   21844   87380  349524
[10] 1398100 5592404
> p4 <- 2 * (3 * k + 4)
> p4 
 [1]       32      128      512     2048     8192    32768   131072   524288
 [9]  2097152  8388608 33554432
> n <- log(p4) / log(2)
> n
 [1]  5  7  9 11 13 15 17 19 21 23 25
```


P<sub>3</sub> = 6<cite class='kw'>k</cite> + 6 = 2 (3<cite class='kw'>k</cite> + 3) = 2<sup>n</sup> with <cite class='kw'>k</cite> and <cite class='kw'>n</cite> &isin; <cite class='math_N'></cite><sup>*</sup>. This equation has no solution because 2 and 3 are primes and therefore no power of 2 can be expressed as the result of a multiplication by 3. 

<span class='do'>
**Third important result**  
I have now shown that P<sub>2</sub> generates all the power of 2, with exponent being even, starting from <cite class='kw'>4</cite> and P<sub>4</sub> generates all the power of <cite class='kw'>2</cite>, with exponent being odd, starting from <cite class='kw'>5</cite>. Since P<sub>1</sub> contains values <cite class='kw'>2</cite>, <cite class='kw'>4</cite> and <cite class='kw'>8</cite>, the partition covers all the power of <cite class='kw'>2</cite>, for exponent greater or equal to <cite class='kw'>1</cite>. 
</span>

### Collatz sequence relation to partition

Let's consider any odd number <cite class='kw'>i</cite> <cite class='math_gt'></cite><cite class='kw'>9</cite>. This number is the input to the Collatz sequence.  

As it is odd, I apply <cite class='kw'>&omega;</cite>.  

<cite class='kw'>&omega;</cite><sub>2</sub> = 3 <cite class='kw'>&omega;</cite><sub>1</sub> + 1 = 3 <cite class='kw'>i</cite> + 1 = 3 (<cite class='kw'>i</cite> - 1) + 4 = 6 <cite class='kw'>k</cite> + 4 &isin; P<sub>2</sub> because <cite class='kw'>i</cite> - 1 is forcibly even and so can be expressed as <cite class='kw'>i</cite> - 1 = 2 <cite class='kw'>k</cite>  

Now let's apply inverse <cite class='kw'>inv(&eta;)</cite> to find the antecedent of <cite class='kw'>&omega;</cite><sub>2</sub>. Instead of dividing by <cite class='kw'>2</cite>, I'll multiply by <cite class='kw'>2</cite>. This brings  

<cite class='kw'>inv(&eta;)</cite><sub>3</sub> = 2 * <cite class='kw'>&omega;</cite><sub>2</sub> = 2 * (6<cite class='kw'>k</cite> + 4) = 12 <cite class='kw'>k</cite> + 8 = 6 <cite class='kw'>2k</cite> + 8 &isin; P<sub>4</sub>.  

<span class='do'>
**Fourth important result**  
This proves that all antecedents of P<sub>2</sub> come from P<sub>4</sub>. So, proving Collatz convergence for one or the other will be sufficient to prove Collatz sequence converges.
</span>


### Collatz sequence study for starting number in P<sub>2</sub>

P<sub>2</sub> is even. So, I'll apply <cite class='kw'>&eta;</cite>.  


<cite class='kw'>&eta;</cite><sub>2</sub> = <cite class='kw'>i</cite> / 2 = (6 <cite class='kw'>k</cite> + 4 ) / 2 =  3 <cite class='kw'>k</cite> + 2.  

Let's consider <cite class='kw'>k</cite> as odd. So, I will apply in sequence <cite class='kw'>&omega;</cite> and <cite class='kw'>&eta;</cite>.  

<cite class='kw'>&omega;</cite><sub>3</sub> = 3 (3 <cite class='kw'>k</cite> + 2) + 1 = 9 <cite class='kw'>k</cite> + 7  

<cite class='kw'>&eta;</cite><sub>4</sub> = <cite class='kw'>&omega;</cite><sub>3</sub> / 2 =  (9<cite class='kw'>k</cite> + 7) / 2  

<cite class='kw'>&omega;</cite><sub>5</sub> = 3 ((9 <cite class='kw'>k</cite> + 7) / 2)+ 1 = (27<cite class='kw'>k</cite> + 23) / 2  

<cite class='kw'>&eta;</cite><sub>6</sub> = <cite class='kw'>&omega;</cite><sub>3</sub> / 2 =  (27<cite class='kw'>k</cite> + 23) / 4  

<cite class='kw'>&omega;</cite><sub>7</sub> = 3 ((27 <cite class='kw'>k</cite> + 23) / 4)+ 1 = (81<cite class='kw'>k</cite> + 73) / 4  

<cite class='kw'>&eta;</cite><sub>8</sub> = <cite class='kw'>&omega;</cite><sub>3</sub> / 2 =  (81<cite class='kw'>k</cite> + 73) / 8  

 

```r
> constant <- function(n) {
+   if (n == 1) return(2)
+   3 * constant(n - 1) + if (n > 2) 2^(n - 2) else 1
+ }
> sapply(1:20, constant)
 [1]          2          7         23         73        227        697
 [7]       2123       6433      19427      58537     176123     529393
[13]    1590227    4774777   14332523   43013953  129074627  387289417
[19] 1161999323 3486260113
```










