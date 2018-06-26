---
title: Collatz Sequence - part 6
hidden: false
categories: mathematics EN
tags: mathematics R computing 
author: neonira
permalink: math_cs_6
output:
  html_document
---
Proof of Collatz sequence convergence. 

## Some reminders first

Remember Collatz sequence definition
![collatz definition](/images/maths/collatz/cs.png)

Let's divide the Collatz sequence into two independent suites, for analysis convenience.   
First suite <cite class='kw'> &omega;</cite> is for <cite class='kw odd'></cite> numbers: <cite class='kw'> &omega;<sub>n + 1</sub></cite> = 3 <cite class='kw'> &omega;<sub>n</sub></cite> + 1    
Second suite <cite class='kw'> &eta;</cite> is for <cite class='kw even'></cite> numbers: 
<cite class='kw'> &eta;<sub>n + 1</sub></cite> = <cite class='kw'> &eta;<sub>n</sub></cite> / 2  


## Resolution for numbers from 2 to 11

### resolution graph
First, let's proceed to an exploratory analysis, and show results as a graph

![The resolution graph](/images/maths/collatz/2-11serie.png)

### computation 
Doing computation, here is a summary for number 9, that covers all the cases for numbers between 2 and 11. 

```r
> cs(9)
 [1] 9 28 14 7 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1
```

<span class='do'>
**First important result**  
Therefore, by calculus, I proved that all the numbers from 2 to 11, provides 1 as final output of Collatz sequence. 
</span>


## Assumption

Let's consider the Collatz sequence to be proven up to a given number <cite class='kw'>z</cite>. This means that Collatz sequence is proven to be converging for any number <cite class='kw'>m</cite> &isin; <cite class='math_N'></cite> respecting <cite class='kw'>m</cite> <cite class='math_lt'></cite> <cite class='kw'>z</cite>. 

## Proof for any <cite class='kw even'></cite> number <cite class='kw'>e</cite> verifying <cite class='kw'>z</cite> <cite class='math_lt'></cite> <cite class='kw'>e</cite> <cite class='math_lt'></cite> <cite class='kw'>2z</cite>

As <cite class='kw'>e</cite> is an <cite class='kw even'></cite> number, then let's apply <cite class='kw'>&eta;</cite>. The result of dividing by two is less than <cite class='kw'>z</cite>, and therefore under the assumption stated above, is proven to be converging. Therefore any even number respecting <cite class='kw'>z</cite> <cite class='math_lt'></cite> <cite class='kw'>e</cite> <cite class='math_lt'></cite> <cite class='kw'>2z</cite> is proven to be a valid input for Collatz sequence to be converging.  

Now that it is proven for <cite class='kw even'></cite> number <cite class='kw'>z</cite> <cite class='math_lt'></cite> <cite class='kw'>e</cite> <cite class='math_lt'></cite> <cite class='kw'>2z</cite>, let's repeat same reasoning with <cite class='kw'>z'</cite> = <cite class='kw'>2z</cite>. This proves that any <cite class='kw even'></cite> number <cite class='kw'>e</cite> respecting <cite class='kw'>z'</cite> <cite class='math_lt'></cite> <cite class='kw'>e</cite> <cite class='math_lt'></cite> <cite class='kw'>2z'</cite> converges. And so on, proving that any <cite class='kw even'></cite> number converges.

Reasoning by recurrence, I got
1. first <cite class='kw even'></cite> number that is 2 converges to 1 immediately, just applying <cite class='kw'>&eta;</cite>.  
1. any <cite class='kw even'></cite> number verifying <cite class='kw'>z</cite> <cite class='math_lt'></cite> <cite class='kw'>e</cite> <cite class='math_lt'></cite> <cite class='kw'>2z</cite>, whatever is <cite class='kw'>z</cite> converges applying Collatz sequence.

Therefore,

<span class='do'>
**Second important result**  
All the <cite class='kw even'></cite> numbers, converges to 1 as final output of Collatz sequence. 
</span>

## Proof for any <cite class='kw odd'></cite> number <cite class='kw'>o</cite>

### Direct proof
As <cite class='kw'>o</cite> is an <cite class='kw odd'></cite> number, then let's apply <cite class='kw'>&omega;</cite>. I already demonstrated that applying <cite class='kw'>&omega;</cite> to and <cite class='kw odd'></cite> number provides an <cite class='kw even'></cite> number. As I have proven here above, that any <cite class='kw even'></cite> number brings convergence, therefore,  all the <cite class='kw odd'></cite> numbers also bring convergence. 

### Calculus proof

As <cite class='kw'>o</cite> is an <cite class='kw odd'></cite> number, it can be written as <cite class='kw'>ah</cite> + <cite class='kw'>bt</cite> +<cite class='kw'>u</cite>. And as it is an <cite class='kw odd'></cite> number, then let's apply <cite class='kw'>&omega;</cite> and <cite class='kw'>&eta;</cite>. 

starting number cs<sub>1</sub> = <cite class='kw'>o</cite> = 2<cite class='kw'>p</cite> + 1 = <cite class='kw'>ah</cite> + <cite class='kw'>bt</cite> +<cite class='kw'>u</cite>  
cs<sub>3</sub> = <cite class='kw'>&eta;</cite>(<cite class='kw'>&omega;</cite>(s)) = <cite class='kw'>&eta;</cite>(<cite class='kw'>&omega;</cite>(2<cite class='kw'>p</cite> + 1)) = 3<cite class='kw'>p</cite> + 2 = <cite class='kw'>&eta;</cite>(<cite class='kw'>&omega;</cite>(<cite class='kw'>ah</cite> + <cite class='kw'>bt</cite> +<cite class='kw'>u</cite>)) = (3<cite class='kw'>ah</cite> + 3<cite class='kw'>bt</cite> + (<cite class='kw'>3u </cite>+ 1)) / 2    

<table>
<thead>
<tr>
<th>cs#</th><th>formulae</th><th>hundreds</th><th>tens</th><th>unit</th><th>comment</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td><td><cite class='kw'>ah</cite> + <cite class='kw'>bt</cite> +<cite class='kw'>u</cite></td><td><cite class='kw'>a</cite></td><td><cite class='kw'>b</cite></td><td><cite class='kw'>u</cite></td><td><cite class='kw'>u</cite> &isin; {<span class='digit digit1'></span>, <span class='digit digit3'></span>, <span class='digit digit5'></span>, <span class='digit digit7'></span>, <span class='digit digit9'></span>}</td></tr>

<tr><td>3</td><td>(3<cite class='kw'>ah</cite> + 3<cite class='kw'>bt</cite> + (<cite class='kw'>3u </cite>+ 1)) / 2</td><td>3<cite class='kw'>a</cite> / 2</td>
<td>
3<cite class='kw'>b</cite> / 2 <br>
3<cite class='kw'>b</cite> / 2 + 1<br>
3<cite class='kw'>b</cite> / 2 + 1<br>
3<cite class='kw'>b</cite> / 2 + 2<br>
3<cite class='kw'>b</cite> / 2 + 2<br>
</td>
<td>(3<cite class='kw'>u</cite> + 1) / 2</td>
<td>
<span class='digit digit1'></span> <cite class='arrow'></cite> <span class='digit digit2'></span>  <cite class='kw even'></cite> number<br>
<span class='digit digit3'></span> <cite class='arrow'></cite> <span class='digit digit5'></span> <cite class='kw odd'></cite> number<br>
<span class='digit digit5'></span> <cite class='arrow'></cite> <span class='digit digit8'></span> <cite class='kw even'></cite> number<br>
<span class='digit digit7'></span> <cite class='arrow'></cite> <span class='digit digit1'></span> <cite class='kw odd'></cite> number<br>
<span class='digit digit9'></span> <cite class='arrow'></cite> <span class='digit digit4'></span> <cite class='kw even'></cite> number<br>
</td></tr>
</tbody>
</table>


Let's focus on cs<sub>3</sub>, when it outputs an <cite class='kw even'></cite> number. From calculus, shown on previous table, the cases happen when cs<sub>1</sub> has a starting unit digit that is amongst <span class='digit digit1'></span>, <span class='digit digit5'></span> or <span class='digit digit9'></span>. As we have previously proven that any <cite class='kw even'></cite> number converges, this means that any <cite class='kw odd'></cite> number finishing with digit <span class='digit digit1'></span>, <span class='digit digit5'></span> or <span class='digit digit9'></span> converges.  

Now remain two cases, when cs<sub>1</sub> has a starting unit digit that is among <span class='digit digit3'></span> or <span class='digit digit7'></span>. Here, let's apply again <cite class='kw'>&omega;</cite> and <cite class='kw'>&eta;</cite> as those numbers are <cite class='kw odd'></cite>. Reusing previous table, the commutation will prove 
- cs<sub>1</sub> <span class='digit digit3'></span> <cite class='arrow'></cite> cs<sub>3</sub> <span class='digit digit5'></span> <cite class='arrow'></cite> cs<sub>5</sub><span class='digit digit8'></span> <cite class='kw even'></cite> number
- cs<sub>1</sub> <span class='digit digit7'></span> <cite class='arrow'></cite>  cs<sub>3</sub> <span class='digit digit1'></span> <cite class='arrow'></cite> cs<sub>5</sub><span class='digit digit2'></span> <cite class='kw even'></cite> number. 

Again, as we have previously proven that any <cite class='kw even'></cite> number converges, this means that any <cite class='kw odd'></cite> number finishing with digit <span class='digit digit3'></span> or <span class='digit digit7'></span> converges.

<span class='do'>
**Third important result**  
All the <cite class='kw odd'></cite> numbers, converges to 1 as final output of Collatz sequence. 
</span>


## Summary

Simply put, I have proven 

1. all the numbers from 2 to 11 converges to 1. Proven by calculus
2. all <cite class='kw even'></cite> numbers converges to 1. Proven by recurrence
3. all <cite class='kw odd'></cite> numbers converges to 1. Proven by reusing <cite class='kw even'></cite> numbers convergence, based on calculus. 

Therefore, proof of Collatz sequence is achieved. Your comments, remarks and feebacks are welcome. Use comment zone to do so. 


##### Note
All calculus done using <cite class='kw'>R</cite> language.


