---
title: Collatz Sequence - part 2
hidden: false
categories: mathematics
tags: mathematics R computing 
author: neonira
permalink: math_cs_2
output:
  html_document:
    number_sections: true
---
On [first post part](math_cs_1) , we got some intuition about Collatz sequence], that seems to be unproven yet. Let's try to prove it mathematically.   

## Some mathematic reminders

### Canonical form a a natural integer

We name <cite class='kw'>canonical form</cite> any natural integer <cite class='kw'>n</cite>, written under one of following forms
* <cite class='kw'>n</cite> = 10 <cite class='kw'>t</cite> + <cite class='kw'>u</cite> 
* <cite class='kw'>n</cite> = 100 <cite class='kw'>h</cite> + 10 <cite class='kw'>t</cite> + <cite class='kw'>u</cite>

Note that <cite class='kw'>n, h, d, u &isin; &#x2115;</cite>&nbsp;&nbsp;&nbsp;<cite class='comment'>where h represents hundreds, t represents tens, and u to represents units</cite>.  

Unless otherwise specified, the expression <cite class='kw'>canonical form</cite> refers always to the first form.  

### Determining parity of a number

By definition, an <cite class='kw even'></cite> number <cite class='kw'>n</cite> can be written as <cite class='kw'>n</cite> = 2 <cite class='kw'>p</cite> &nbsp;&nbsp;&nbsp; <cite class='kw'>n, p &isin; &#x2115;</cite>&nbsp;&nbsp;&nbsp;<cite class='comment'>note that n is <cite class='kw even'></cite>, but we have no information about p that can be <cite class='kw even'></cite> or <cite class='kw odd'></cite></cite>.  


By definition, an <cite class='kw odd'></cite> number<cite class='kw'>n</cite> can be written as <cite class='kw'>n</cite> = 2 <cite class='kw'>p</cite> + 1 &nbsp;&nbsp;&nbsp; <cite class='kw'>n, p &isin; &#x2115;</cite>&nbsp;&nbsp;&nbsp;<cite class='comment'>note that n is <cite class='kw even'></cite>, but we have no information about p that can be <cite class='kw even'></cite> or <cite class='kw odd'></cite></cite>.  

#### Parity of a sum of two natural integers

Using the shown definitions, I can demonstrate following table of truth for parity addition of two natural integers  

<table>
<thead>
<tr>
<td>sum <cite class='kw'>p</cite> + <cite class='kw'>q</cite></td>
<td><cite class='kw'>p</cite> is <cite class='kw even'></cite></td>
<td><cite class='kw'>p</cite> is <cite class='kw odd'></cite></td>
</tr>
</thead>
<tbody>
<tr>
<td><cite class='kw'>q</cite> is <cite class='kw even'></cite></td>
<td>sum is <cite class='kw even'></cite></td>
<td>sum is <cite class='kw odd'></cite></td>
</tr>
<tr>
<td><cite class='kw'>q</cite> is <cite class='kw odd'></cite></td>
<td>sum is <cite class='kw odd'></cite></td>
<td>sum is <cite class='kw even'></cite></td>
</tr>
</tbody>
</table>

So, given one number <cite class='kw'>p</cite>, to determine the parity of the sum with <cite class='kw'>q</cite>, we just have to consider
1. the parity of <cite class='kw'>q</cite> when <cite class='kw'>p</cite> is <cite class='kw even'></cite>
1. the negation of the parity of <cite class='kw'>q</cite>, that is <cite class='kw' style='font-weight:bold'>&#172;q</cite>, when <cite class='kw'>p</cite> is <cite class='kw odd'></cite>

#### Parity of a product of two natural integers

Using the shown definitions, I can demonstrate following table of truth for parity multipliction of two natural integers  

<table>
<thead>
<tr>
<td>multiplication <cite class='kw'>p</cite> * <cite class='kw'>q</cite></td>
<td><cite class='kw'>p</cite> is <cite class='kw even'></cite></td>
<td><cite class='kw'>p</cite> is <cite class='kw even'></cite></td>
</tr>
</thead>
<tbody>
<tr>
<td><cite class='kw'>q</cite> is <cite class='kw even'></cite></td>
<td>multiplication is <cite class='kw even'></cite></td>
<td>multiplication is <cite class='kw even'></cite></td>
</tr>
<tr>
<td><cite class='kw'>q</cite> is <cite class='kw odd'></cite></td>
<td>multiplication is <cite class='kw even'></cite></td>
<td>multiplication is <cite class='kw odd'></cite></td>
</tr>
</tbody>
</table>

So, the production of two natural numbers is <cite class='kw odd'></cite> only when both of them are <cite class='kw odd'></cite>.


## Digit mutation proof

Remember Collatz sequence definition
![collatz definition](/images/maths/collatz/cs.png)

### Digit mutation proof for <cite class='kw even'></cite> numbers

In this part, as all numbers are <cite class='kw even'></cite>, I will apply division by <cite class='kw'>2</cite>. 
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
<td><span class='digit digit0'></span></td>
<td><cite class='kw even'></cite></td>
<td>5 <cite class='kw'>t</cite></td>
<td>
10 <cite class='kw'>p</cite> + 0 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 5 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p</cite> + 1<br>
</td>
<td>0 when <cite class='kw'>d</cite> is <cite class='kw even'></cite> <br>5 when <cite class='kw'>t</cite> is <cite class='kw odd'></cite></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 2</td>
<td><span class='digit digit2'></span></td>
<td><cite class='kw even'></cite></td>
<td>5 <cite class='kw'>t</cite> + 1</td>
<td>
10 <cite class='kw'>p</cite> + 1 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 6 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>1 when <cite class='kw'>t</cite> is <cite class='kw even'></cite> <br>6 when <cite class='kw'>t</cite> is <cite class='kw odd'></cite></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 4</td>
<td><span class='digit digit4'></span></td>
<td><cite class='kw even'></cite></td>
<td>5 <cite class='kw'>t</cite> + 2</td>
<td>
10 <cite class='kw'>p</cite> + 2 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 7 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>2 when <cite class='kw'>t</cite> is <cite class='kw even'></cite> <br>7 when <cite class='kw'>t</cite> is <cite class='kw odd'></cite></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 6</td>
<td><span class='digit digit6'></span></td>
<td><cite class='kw even'></cite></td>
<td>5 <cite class='kw'>t</cite> + 3</td>
<td>
10 <cite class='kw'>p</cite> + 3 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 8 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>3 when <cite class='kw'>t</cite> is <cite class='kw even'></cite> <br>8 when <cite class='kw'>t</cite> is <cite class='kw odd'></cite></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 8</td>
<td><span class='digit digit8'></span></td>
<td><cite class='kw even'></cite></td>
<td>5 <cite class='kw'>t</cite> + 4</td>
<td>
10 <cite class='kw'>p</cite> + 4 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite><br>
10 <cite class='kw'>p</cite> + 9 &nbsp;&nbsp;&nbsp; <cite class='kw'>t</cite> = 2 <cite class='kw'>p </cite> + 1
</td>
<td>4 when <cite class='kw'>t</cite> is <cite class='kw even'></cite> <br><cite class='kw'>9</cite> when <cite class='kw'>t</cite> is <cite class='kw odd'></cite></td>
</tr>

</tbody>
</table>

So, we have proven several things, for <cite class='kw even'></cite> numbers
1. When applying Collatz sequence to an <cite class='kw even'></cite> number, produced result will fork on two different digits depending of the parity of <cite class='kw'>t</cite>. Note, the special case of <cite class='kw'>0</cite>, that is the only case with self loop. 
1. As we divide, by <cite class='kw'>2</cite>, the result is strictly less than the input. 


### Digit mutation proof for <cite class='kw odd'></cite> numbers

In this part, as all numbers are <cite class='kw odd'></cite>, I will apply apply by 3 <cite class='kw'>&upsilon;<sub>n</sub></cite> + 1. 
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
<td><span class='digit digit1'></span></td>
<td><cite class='kw odd'></cite></td>
<td>30 <cite class='kw'>t</cite> + 4</td>
<td>
10 (3 <cite class='kw'>t</cite>) + 4
</td>
<td><span class='digit digit4'></span></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 3</td>
<td><span class='digit digit3'></span></td>
<td><cite class='kw odd'></cite></td>
<td>30 <cite class='kw'>t</cite> + 10</td>
<td>
10 (3 <cite class='kw'>t</cite> + 1) + 0
</td>
<td><span class='digit digit0'></span></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 5</td>
<td><span class='digit digit5'></span></td>
<td><cite class='kw odd'></cite></td>
<td>30 <cite class='kw'>t</cite> + 16</td>
<td>
10 (3 <cite class='kw'>t</cite> + 1) + 6
</td>
<td><span class='digit digit6'></span></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + 7</td>
<td><span class='digit digit7'></span></td>
<td><cite class='kw odd'></cite></td>
<td>30 <cite class='kw'>t</cite> + 22</td>
<td>
10 (3 <cite class='kw'>t</cite> + 2) + 2 
</td>
<td><span class='digit digit2'></span></td>
</tr>

<tr>
<td>10 <cite class='kw'>t</cite> + <cite class='kw'>9</cite></td>
<td><span class='digit digit9'></span></td>
<td><cite class='kw odd'></cite></td>
<td>30 <cite class='kw'>t</cite> + 28</td>
<td>
10 (3 <cite class='kw'>t</cite> + 2) + 8 
</td>
<td><span class='digit digit8'></span></td>
</tr>

</tbody>
</table>


So, are now proven several things, for <cite class='kw odd'></cite> numbers
1. When applying Collatz sequence to an <cite class='kw odd'></cite> number, produced result will always be an <cite class='kw even'></cite> number. This implies that when applying Collatz sequence, we will never apply twice in a run the Collatz sequence <cite class='kw odd'></cite> rule.   
1. The result is always greater than the input for <cite class='kw odd'></cite> numbers

## Suite analysis
Let's focus now on suite analysis, has this will bring many insights on the Collatz Sequence results. 

### Suite definitions

Let's divide the Collatz sequence into two independent suites, for analysis convenience.   
First suite is for <cite class='kw odd'></cite> numbers: <cite class='kw'> &omega;<sub>n + 1</sub></cite> = 3 <cite class='kw'> &omega;<sub>n</sub></cite> + 1    
Second suite is for <cite class='kw even'></cite> numbers: 
<cite class='kw'> &eta;<sub>n + 1</sub></cite> = <cite class='kw'> &eta;<sub>n</sub></cite> / 2  

By convention, the indice <sub>n</sub> starts at 1. 

### Calculus formulaes

We need a formulae that provides the n<sup>th</sup> result, directly from the input.  

For <cite class='kw even'></cite> numbers, it is quite obvious, as 
<cite class='kw'> &eta;<sub>k</sub></cite> = <cite class='kw'> &eta;<sub>1</sub></cite> / 2<sup>k</sup> with <cite class='kw'>k</cite> being the number of times we apply the transformation, will provide the result.  

For <cite class='kw odd'></cite> numbers, suite analysis will show that 
<cite class='kw'> &omega;<sub>k</sub></cite> = <cite class='kw'> &phi;<sub>k</sub></cite> + <cite class='kw'> &sigma;<sub>k</sub></cite>

* with <cite class='kw'> &phi;<sub>k</sub></cite> = 3<sup>k</sup> <cite class='kw'>&phi;<sub>1</sub></cite>
* <cite class='kw'> &sigma;<sub>k</sub></cite> = <cite class = 'symbol'>&Sigma;</cite><cite class = 'kw'><sub>i = 1</sub><sup>k</sup> 3<sup>i - 1</sup></cite>.


### Parity analysis 

#### parity analysis of <cite class='kw'> &eta;<sub>k</sub></cite>
As <cite class='kw'> &eta;<sub>k</sub></cite> starts forcibly with <cite class='kw'> &eta;<sub>1</sub></cite> being <cite class='kw even'></cite>, the recurring process of division by 2 repeats while <cite class='kw'> &eta;<sub>k</sub></cite> is <cite class='kw even'></cite> and stops immediately when not. In the worst case, we execute a single division by 2.  


#### parity analysis of <cite class='kw'> &omega;<sub>k</sub></cite>

As this suite is composed of the sum of 2 suites, we will use the addition parity table. 

##### parity analysis of <cite class='kw'> &phi;<sub>k</sub></cite>

As <cite class='kw'> &phi;<sub>k</sub></cite> starts forcibly with <cite class='kw'> &phi;<sub>1</sub></cite> being <cite class='kw odd'></cite>, the recurring process of multiplication by 3<sup>k</sup> that is always <cite class='kw odd'></cite> too, brings always an <cite class='kw odd'></cite> result. 

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
<cite class='kw'>&sigma;<sub>4n + 1</sub></cite> ends with digit <span class='digit digit1'></span>  
<cite class='kw'>&sigma;<sub>4n + 2</sub></cite> ends with digit <span class='digit digit3'></span>  
<cite class='kw'>&sigma;<sub>4n + 3</sub></cite> ends with digit <span class='digit digit9'></span>  
<cite class='kw'>&sigma;<sub>4n + 4</sub></cite> ends with digit <span class='digit digit7'></span>  
Sum of this four ending digits turns to be <cite class='kw'>20</cite>. 
</span>

So the parity of suite <cite class='kw'>&sigma;<sub>n</sub></cite> follows a pattern that is 
<cite class='kw odd'></cite> and then <cite class='kw even'></cite>, and repeat this sequence.  

More precisely, we have parity(<cite class='kw'>&phi;<sub>2 n + 1</sub></cite>) = parity(<cite class='kw'>&phi;<sub>1</sub></cite>) and parity(<cite class='kw'>&phi;<sub>2 n</sub></cite>) =
&#172; <!-- neg--> (parity(<cite class='kw'>&phi;<sub>1</sub></cite>)).  


Therefore, the suite <cite class='kw'>&omega;<sub>n</sub></cite> that is the addition of 2 suites,  <cite class='kw'>&phi;<sub>n</sub></cite> that is always <cite class='kw odd'></cite> and <cite class='kw'>&sigma;<sub>n</sub></cite> that is an alternate parity suite starting with an <cite class='kw odd'></cite> value. 
In short, <cite class='kw'>&omega;<sub>n</sub></cite> has the same parity as <cite class='kw'>&sigma;<sub>n</sub></cite>.

### Digit mutation conclusion 

The canonical forms used on paragraphs 2.1 and 2.2, covers individually all the numbers that end with a digit from <span class='digit digit0'></span> to <span class='digit digit9'></span>. They form a partition of &#x2115;. This partition is fully covering &#x2115; as each number ends by one of the 10 digits.  

One way to understand the digit mutation tables, is to consider the canonical form as a generative suite of the input number, and applying <cite class='kw'>&eta;</cite> or <cite class='kw'>&omega;</cite> will create a generative suite of the output number that will end with a predicted digit. 






