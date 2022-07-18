---
layout: post
title: R - Math - Collatz sequence part II
category: category-rmetaverse
summary: overview and discovery of the Collatz sequence
image: images/maths/collatz/cs.png
# comments: true
permalink: rm-r-math-2
---

On [first post part](https://neonira.github.io/rm-r-math-1) , we got some intuition about Collatz sequence], that seems to be unproven yet. Let's try to prove it mathematically.   

## Some mathematic reminders

### Canonical form a a natural integer

We name <cite class='kw'>canonical form</cite> any natural integer <cite class='kw'>n</cite>, written under one of following forms
* <cite class='kw'>n</cite> = 10 <cite class='kw'>t</cite> + <cite class='kw'>u</cite> 
* <cite class='kw'>n</cite> = 100 <cite class='kw'>h</cite> + 10 <cite class='kw'>t</cite> + <cite class='kw'>u</cite>

Note that <cite class='kw'>n, h, d, u &isin; &#x2115;</cite>&nbsp;&nbsp;&nbsp;<cite class='comment'>where h represents hundreds, t represents tens, and u to represents units</cite>.  

Unless otherwise specified, the expression <cite class='kw'>canonical form</cite> refers always to the first form.  

### Determining parity of a number

By definition, an even number <cite class='kw'>n</cite> can be written as <cite class='kw'>n</cite> = 2 <cite class='kw'>p</cite> &nbsp;&nbsp;&nbsp; <cite class='kw'>n, p &isin; &#x2115;</cite>&nbsp;&nbsp;&nbsp;<cite class='comment'>note that n is even, but we have no information about p that can be even or odd</cite>.  


By definition, an odd number<cite class='kw'>n</cite> can be written as <cite class='kw'>n</cite> = 2 <cite class='kw'>p</cite> + 1 &nbsp;&nbsp;&nbsp; <cite class='kw'>n, p &isin; &#x2115;</cite>&nbsp;&nbsp;&nbsp;<cite class='comment'>note that n is odd, but we have no information about p that can be even or odd</cite>.  

#### Parity of a sum of two natural integers

Using the shown definitions, I can demonstrate following table of truth for parity addition of two natural integers  

<table>
<thead>
<tr>
<td>sum <cite class='kw'>p</cite> + <cite class='kw'>q</cite></td>
<td><cite class='kw'>p</cite> is even</td>
<td><cite class='kw'>p</cite> is odd</td>
</tr>
</thead>
<tbody>
<tr>
<td><cite class='kw'>q</cite> is even</td>
<td>sum is even</td>
<td>sum is odd</td>
</tr>
<tr>
<td><cite class='kw'>q</cite> is odd</td>
<td>sum is odd</td>
<td>sum is even</td>
</tr>
</tbody>
</table>

So, given one number <cite class='kw'>p</cite>, to determine the parity of the sum with <cite class='kw'>q</cite>, we just have to consider
1. the parity of <cite class='kw'>q</cite> when <cite class='kw'>p</cite> is even
1. the negation of the parity of <cite class='kw'>q</cite>, that is <cite class='kw' style='font-weight:bold'>&#172;q</cite>, when <cite class='kw'>p</cite> is odd

#### Parity of a product of two natural integers

Using the shown definitions, I can demonstrate following table of truth for parity multipliction of two natural integers  

<table>
<thead>
<tr>
<td>multiplication <cite class='kw'>p</cite> * <cite class='kw'>q</cite></td>
<td><cite class='kw'>p</cite> is even</td>
<td><cite class='kw'>p</cite> is odd</td>
</tr>
</thead>
<tbody>
<tr>
<td><cite class='kw'>q</cite> is even</td>
<td>multiplication is even</td>
<td>multiplication is even</td>
</tr>
<tr>
<td><cite class='kw'>q</cite> is odd</td>
<td>multiplication is even</td>
<td>multiplication is odd</td>
</tr>
</tbody>
</table>

So, the production of two natural numbers is odd only when both of them are odd.


## Digit mutation proof

Remember Collatz sequence definition
![collatz definition](images/maths/collatz/cs.png)

### Digit mutation proof for even numbers

In this part, as all numbers are even, I will apply division by <cite class='kw'>2</cite>. 
<table>
<thead>
<tr style='font-weight:bold'>
<td colspan='3'> <cite class='kw'> &upsilon;<sub>n</sub></cite></td>
<td colspan='3'> result of Collatz rule application</td>
</tr>
<tr style='font-weight:bold;font-style:oblique;font-size:.8em'>
<td>canonical form</td>
<td>digit</td>
<td>parity</td>
<td>calculus formula</td>
<td>canonical form</td>
<td>digit</td>
</tr>
</thead>
<tbody>
<tr>
<td>10 <cite class='kw'>t</cite> + 0</td>
<td>0</td>
<td>even</td>
<td>5 <cite class='kw'>t</cite></td>
<td>
10 <cite class='kw'>p</cite> + 0 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 5 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p</cite> + 1<br>
</td>
<td>0 when <cite class='kw'>d</cite> is even <br>5 when <cite class='kw'>t</cite> is odd</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 2</td>
<td>2</td>
<td>even</td>
<td>5 <cite class='kw'>t</cite> + 1</td>
<td>
10 <cite class='kw'>p</cite> + 1 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 6 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>1 when <cite class='kw'>t</cite> is even <br>6 when <cite class='kw'>t</cite> is odd</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 4</td>
<td>4</td>
<td>even</td>
<td>5 <cite class='kw'>t</cite> + 2</td>
<td>
10 <cite class='kw'>p</cite> + 2 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 7 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>2 when <cite class='kw'>t</cite> is even <br>7 when <cite class='kw'>t</cite> is odd</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 6</td>
<td>6</td>
<td>even</td>
<td>5 <cite class='kw'>t</cite> + 3</td>
<td>
10 <cite class='kw'>p</cite> + 3 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 8 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>3 when <cite class='kw'>t</cite> is even <br>8 when <cite class='kw'>t</cite> is odd</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 8</td>
<td>8</td>
<td>even</td>
<td>5 <cite class='kw'>t</cite> + 4</td>
<td>
10 <cite class='kw'>p</cite> + 4 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 9 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>4 when <cite class='kw'>t</cite> is even <br><cite class='kw'>9</cite> when <cite class='kw'>t</cite> is odd</td>
</tr>

</tbody>
</table>

So, we have proven several things, for even numbers
1. When applying Collatz sequence to an even number, produced result will fork on two different digits depending of the parity of <cite class='kw'>t</cite>. Note, the special case of <cite class='kw'>0</cite>, that is the only case with self loop. 
1. As we divide, by <cite class='kw'>2</cite>, the result is strictly less than the input. 


### Digit mutation proof for odd numbers

In this part, as all numbers are odd, I will apply apply by 3 <cite class='kw'>&upsilon;<sub>n</sub></cite> + 1. 
<table>
<thead>
<tr style='font-weight:bold'>
<td colspan='3'> <cite class='kw'> &upsilon;<sub>n</sub></cite></td>
<td colspan='3'> result of Collatz rule application</td>
</tr>
<tr style='font-weight:bold;font-style:oblique;font-size:.8em'>
<td>canonical form</td>
<td>digit</td>
<td>parity</td>
<td>calculus formula</td>
<td>canonical form</td>
<td>digit</td>
</tr>
</thead>
<tbody>
<tr>
<td>10 <cite class='kw'>t</cite> + 1</td>
<td>1</td>
<td>odd</td>
<td>30 <cite class='kw'>t</cite> + 4</td>
<td>
10 (3 <cite class='kw'>t</cite>) + 4
</td>
<td>4</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 3</td>
<td>3</td>
<td>odd</td>
<td>30 <cite class='kw'>t</cite> + 10</td>
<td>
10 (3 <cite class='kw'>t</cite> + 1) + 0
</td>
<td>0</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 5</td>
<td>5</td>
<td>odd</td>
<td>30 <cite class='kw'>t</cite> + 16</td>
<td>
10 (3 <cite class='kw'>t</cite> + 1) + 6
</td>
<td>6</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 7</td>
<td>7</td>
<td>odd</td>
<td>30 <cite class='kw'>t</cite> + 22</td>
<td>
10 (3 <cite class='kw'>t</cite> + 2) + 2 
</td>
<td>2</td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + <cite class='kw'>9</cite></td>
<td>9</td>
<td>odd</td>
<td>30 <cite class='kw'>t</cite> + 28</td>
<td>
10 (3 <cite class='kw'>t</cite> + 2) + 8 
</td>
<td>8</td>
</tr>

</tbody>
</table>


So, are now proven several things, for odd numbers
1. When applying Collatz sequence to an odd number, produced result will always be an even number. This implies that when applying Collatz sequence, we will never apply twice in a run the Collatz sequence odd rule.   
1. The result is always greater than the input for odd numbers

## Suite analysis
Let's focus now on suite analysis, has this will bring many insights on the Collatz Sequence results. 

### Suite definitions

Let's divide the Collatz sequence into two independent suites, for analysis convenience.   
First suite is for odd numbers: <cite class='kw'> &omega;<sub>n + 1</sub></cite> = 3 <cite class='kw'> &omega;<sub>n</sub></cite> + 1    
Second suite is for even numbers: 
<cite class='kw'> &eta;<sub>n + 1</sub></cite> = <cite class='kw'> &eta;<sub>n</sub></cite> / 2  

By convention, the indice <sub>n</sub> starts at 1. 

### Calculus formulaes

We need a formulae that provides the n<sup>th</sup> result, directly from the input.  

For even numbers, it is quite obvious, as 
<cite class='kw'> &eta;<sub>k</sub></cite> = <cite class='kw'> &eta;<sub>1</sub></cite> / 2<sup>k</sup> with <cite class='kw'>k</cite> being the number of times we apply the transformation, will provide the result.  

For odd numbers, suite analysis will show that 
<cite class='kw'> &omega;<sub>k</sub></cite> = <cite class='kw'> &phi;<sub>k</sub></cite> + <cite class='kw'> &sigma;<sub>k</sub></cite>

* with <cite class='kw'> &phi;<sub>k</sub></cite> = 3<sup>k</sup> <cite class='kw'>&phi;<sub>1</sub></cite>
* <cite class='kw'> &sigma;<sub>k</sub></cite> = <cite class = 'symbol'>&Sigma;</cite><cite class = 'kw'><sub>i = 1</sub><sup>k</sup> 3<sup>i - 1</sup></cite>.


### Parity analysis 

#### parity analysis of <cite class='kw'> &eta;<sub>k</sub></cite>
As <cite class='kw'> &eta;<sub>k</sub></cite> starts forcibly with <cite class='kw'> &eta;<sub>1</sub></cite> being even, the recurring process of division by 2 repeats while <cite class='kw'> &eta;<sub>k</sub></cite> is even and stops immediately when not. In the worst case, we execute a single division by 2.  


#### parity analysis of <cite class='kw'> &omega;<sub>k</sub></cite>

As this suite is composed of the sum of 2 suites, we will use the addition parity table. 

##### parity analysis of <cite class='kw'> &phi;<sub>k</sub></cite>

As <cite class='kw'> &phi;<sub>k</sub></cite> starts forcibly with <cite class='kw'> &phi;<sub>1</sub></cite> being odd, the recurring process of multiplication by 3<sup>k</sup> that is always odd too, brings always an odd result. 

##### parity analysis of <cite class='kw'> &sigma;<sub>k</sub></cite>

The suite <cite class='kw'>&sigma;<sub>n</sub></cite> results from a sum. The suite is the sum of the successive power of 3, and so <cite class='kw'>&sigma;<sub>n + 1</sub></cite> = <cite class='kw'>&sigma;<sub>n</sub></cite> + 3<sup>n</sup>

```r 
> p <- 0:16
> z <- 3^p
> sapply(p[-1], function(e) sum(z[1:e]))
[1]     1        4       13       40      121      364      1093      3280
[8]  9841    29524    88573   265720   797161  2391484   7174453  21523360
```

<span class='do'> 
**CURIOSITY**: Seems that each forth numbers are multiple of 10.  
<cite class='kw'>&sigma;<sub>4n + 1</sub></cite> ends with digit 1<br/>
<cite class='kw'>&sigma;<sub>4n + 2</sub></cite> ends with digit 3<br/>
<cite class='kw'>&sigma;<sub>4n + 3</sub></cite> ends with digit 5<br/>
<cite class='kw'>&sigma;<sub>4n + 4</sub></cite> ends with digit 7<br/>
Sum of the four computed values turns to be a multiple of <cite class='kw'>20</cite> that is twice 
</span>

So the parity of suite <cite class='kw'>&sigma;<sub>n</sub></cite> follows a pattern that is 
odd and then even, and repeat this sequence.  

More precisely, we have parity(<cite class='kw'>&phi;<sub>2 n + 1</sub></cite>) = parity(<cite class='kw'>&phi;<sub>1</sub></cite>) and parity(<cite class='kw'>&phi;<sub>2 n</sub></cite>) =
&#172; <!-- neg--> (parity(<cite class='kw'>&phi;<sub>1</sub></cite>)).  


Therefore, the suite <cite class='kw'>&omega;<sub>n</sub></cite> that is the addition of 2 suites,  <cite class='kw'>&phi;<sub>n</sub></cite> that is always odd and <cite class='kw'>&sigma;<sub>n</sub></cite> that is an alternate parity suite starting with an odd value. 
In short, <cite class='kw'>&omega;<sub>n</sub></cite> has the same parity as <cite class='kw'>&sigma;<sub>n</sub></cite>.

### Digit mutation conclusion 

The canonical forms used on paragraphs 2.1 and 2.2, covers individually all the numbers that end with a digit from 0 to 9. They form a partition of &#x2115;. This partition is fully covering &#x2115; as each number ends by one of the 10 digits.  

One way to understand the digit mutation tables, is to consider the canonical form as a generative suite of the input number, and applying <cite class='kw'>&eta;</cite> or <cite class='kw'>&omega;</cite> will create a generative suite of the output number that will end with a predicted digit. 






