---
title: Collatz Sequence - part 3
hidden: false
categories: mathematics EN
tags: mathematics R computing 
author: neonira
permalink: math_cs_3
output:
  html_document
---
On [first post](https://neonira.github.io/math_cs_1) and [second post](https://neonira.github.io/math_cs_2) parts, I set-up the mathematical context to prove Collatz conjecture.   

## Cluster analysis

To prove Collatz sequence conjecture, we need some extraneous analysis. Reusing results of digit mutation proof, we know that the transition path from one number to another is driven by its unit digit, and that the transitions are always the same for one digit.

### Cluster definitions

I name cluster a group of transition path from one number to another.

#### Definition of <cite class='kw'>cluster 1</cite>

<cite class='kw'>cluster 1</cite> is made of numbers with unit digit being part of set <cite class='kw' style='font-size:1.1em;'>S<sub>1</sub></cite> = { <span class='digit digit6'></span>, <span class='digit digit3'></span>, <span class='digit digit0'></span>, <span class='digit digit5'></span> }.

#### Definition of <cite class='kw'>cluster 2</cite>

<cite class='kw'>cluster 2</cite> is made of numbers with unit digit being part of set <cite class='kw' style='font-size:1.1em;'>S<sub>2</sub></cite> = { <span class='digit digit8'></span>, <span class='digit digit9'></span> }.

#### Definition of <cite class='kw'>cluster 3</cite>
<cite class='kw'>cluster 3</cite> is made of numbers with unit digit being part of set <cite class='kw' style='font-size:1.1em;'>S<sub>3</sub></cite> = { <span class='digit digit4'></span>, <span class='digit digit7'></span>, <span class='digit digit2'></span>, <span class='digit digit1'></span> }.

<span class='do'> 
**NOTA BENE**: The union of the <cite class='kw'>clusters</cite>, cover all the digit unit cases. So, cluster analysis results will be true whatever the input number considered.  
</span>


## Analysis of <cite class='kw'>cluster 2</cite>

### Collatz sequence analysis 

#### Collatz sequence analysis on numbers ending with digit <span class='digit digit9'></span> 
These numbers can be expressed using canonical form as 10 <cite class='kw'>t</cite> + 9. These numbers are <cite class='kw odd'></cite>.  

So, I apply the <cite class='kw odd'></cite> rule of Collatz sequence. This brings the calculus formulae 30 <cite class='kw'>t</cite> + 28.  

This formulae can be rewritten under canonical form as 10 3<cite class='kw'>t</cite> + 8. Therefore, the result will have a digit <span class='digit digit8'></span>.

##### Focus on tens of <span class='digit digit9'></span> 

Let start from a number ending with digit <cite class='kw'>9</cite>, using <cite class='kw'>&omega;</cite> suite.

<cite class='kw'> &omega;<sub>n + 1</sub></cite> = 3 <cite class='kw'> &omega;<sub>n</sub></cite> + 1 &nbsp;&nbsp;&nbsp; by definition

<cite class='kw'> &omega;<sub>n + 1</sub></cite> = (3 <cite class='kw'> &omega;<sub>n</sub></cite> + 3) + (1 - 3) =  3 (<cite class='kw'> &omega;<sub>n</sub></cite> + 1) - 2   
<cite class='kw'> &omega;<sub>n + 1</sub></cite> =  3 (100 <cite class='kw'>h</cite> + 10 <cite class='kw'>t</cite> + 9 + 1) - 2 = 100 <cite class='kw'>3h</cite> + 10 <cite class='kw'>3t</cite> + 30 - 2 = 100 <cite class='kw'>3h</cite> + 10 <cite class='kw'>3t</cite> + 20 + 8 = 100 <cite class='kw'>3h</cite> + 10 (<cite class='kw'>3t</cite> + 2) + 8

Therefore, input number has <cite class='kw'>t</cite> tens, and output number has 3<cite class='kw'>t</cite> + 2 tens.

#### Collatz sequence analysis on numbers ending with digit <span class='digit digit8'></span> 
These numbers can be expressed using canonical form as 10 <cite class='kw'>t</cite> + 8. These numbers are <cite class='kw even'></cite>.

So, I apply the <cite class='kw even'></cite> rule of Collatz sequence. This brings the calculus formulae 5 <cite class='kw'>t</cite> + 4.  

This formulae can be rewritten under conditions
* t is <cite class='kw even'></cite> so, t = 2p and so the canonical form is 10 <cite class='kw'>p</cite> + 4, leading to digit <span class='digit digit4'></span>
* t is <cite class='kw odd'></cite> so, t = 2p + 1 and so the canonical form is 10 <cite class='kw'>p</cite> + 9, leading to digit <span class='digit digit9'></span>

### Computation analysis 

#### Computation on numbers ending with digit <span class='digit digit9'></span> with <cite class='kw even'></cite> tens

Let's consider the cases where tens are 0, 2, 4, 6, or 8. 
<table>
<thead>
<tr style='font-weight:bold'>
<th colspan='3'> <cite class='kw'> &upsilon;<sub>n</sub></cite></th>
</tr>
<tr style='font-weight:bold;font-style:oblique;font-size:.8em'>
<th>n</th>
<th>n + 1</th>
<th>n + 2</th>
</tr>
</thead>
<tbody>
<tr><td>09</td><td>28</td><td>14</td></tr>
<tr><td>29</td><td>88</td><td>44</td></tr>
<tr><td>49</td><td>148</td><td>74</td></tr>
<tr><td>69</td><td>208</td><td>104</td></tr>
<tr><td>89</td><td>268</td><td>134</td></tr>
</tbody>
</table>

All the n + 2 results, are out of the cluster. This proves by calculus, that any <cite class='kw even'></cite> tens of a number ending with digit <span class='digit digit9'></span> drives the suite to another cluster in just <cite class='step'>2</cite> steps.

#### Computation on numbers ending with digit <span class='digit digit9'></span> with <cite class='kw odd'></cite> tens

Let's consider the cases where tens are 1, 3, 5, 7, or 9. 
<table>
<thead>
<tr style='font-weight:bold'>
<th colspan='4'> <cite class='kw'> &upsilon;<sub>n</sub></cite></th>
</tr>
<tr style='font-weight:bold;font-style:oblique;font-size:.8em'>
<th>n</th>
<th>n + 1</th>
<th>n + 2</th>
<th>comment</th>
</tr>
</thead>
<tbody>
<tr><td>19</td><td>58</td><td>29</td><td>even tens for number ending with digit <span class='digit digit9'></span></td></tr>
<tr><td>39</td><td>118</td><td>59</td><td>loop to case 59 of this table</td></tr>
<tr><td>59</td><td>178</td><td>89</td><td>even tens for number ending with digit <span class='digit digit9'></span></td></tr>
<tr><td>79</td><td>238</td><td>119</td><td>loop to case 19 of this table</td></tr>
<tr><td>99</td><td>298</td><td>149</td><td>even tens for number ending with digit <span class='digit digit9'></span></td></tr>
</tbody>
</table>

So, the numbers <cite class='kw'>19</cite>, <cite class='kw'>59</cite>, and <cite class='kw'>99</cite> will exit the cluster in <cite class='step'>4</cite> steps.  

So, the numbers <cite class='kw'>39</cite>, and <cite class='kw'>79</cite> will exit the cluster in <cite class='step'>6</cite> steps. 

#### Conclusion of computation analysis
I have shown that whatever the number ending by digit <span class='digit digit9'></span>, we can predict the number of steps before exiting the cluster and reaching systematically a number ending by digit <span class='digit digit4'></span>. Here is a summary table

<table>
<thead>
<tr style='font-weight:bold'>
<th colspan='5'> <cite class='kw'> &upsilon;<sub>n</sub></cite></th>
</tr>
<tr style='font-weight:bold;font-style:oblique;font-size:.8em'>
<th>t</th>
<th>u</th>
<th>computation sequence</th>
<th>expansion factor</th>
</tr>
</thead>
<tbody>
<tr>
<td>t is <cite class='kw even'></cite></td>
<td><span class='digit digit9'></span></td>
<td><cite class='kw'> &omega;</cite><cite class='arrow kw'>&eta;</cite></td>
<td>3 / 2 = 1.5</td>
</tr>
<tr>
<td>t is <cite class='kw odd'></cite> &isin; { <span class='digit digit1'></span>, <span class='digit digit5'></span>, <span class='digit digit9'></span> }</td>
<td><span class='digit digit9'></span></td>
<td><cite class='kw'> &omega;</cite><cite class='arrow kw'>&eta;</cite><cite class='arrow kw'> &omega;</cite><cite class='arrow kw'>&eta;</cite></td>
<td>9 / 4 = 2.25</td>
</tr>
<tr>
<td>t is <cite class='kw odd'></cite> &isin; { <span class='digit digit3'></span>, <span class='digit digit7'></span> }</td>
<td><span class='digit digit9'></span></td>
<td><cite class='kw'>&omega;</cite><cite class='arrow kw'>&eta;</cite><cite class='arrow kw'>&omega;</cite><cite class='arrow kw'>&eta;</cite><cite class='arrow kw'>&omega;</cite><cite class='arrow kw'>&eta;</cite></td>
<td>27 / 8 = 3.375</td>
</tr>
</tbody>
</table>

The computation sequence is just showing the order of application of Collatz sequence. 

So the conclusion is whatever the input number ending with digit <span class='digit digit9'></span>, the Collatz sequence will drive its sequence to a number ending with digit <span class='digit digit4'></span> in <cite class='step'>2</cite>, <cite class='step'>4</cite> or <cite class='step'>6</cite> steps.  

Moreover, starting with number ending with digit <span class='digit digit8'></span>, owning an <cite class='kw odd'></cite> number of tens will bring to the sequence from a number ending with digit <span class='digit digit9'></span>. In this case, the expansion factors shown above should be divided by 2.  

The cluster <cite class='kw'>2</cite> is therefore acting as a multiplier of its input. It neither diverges nor converges. It just creates an output number greater than its input number. 


<!--
### Entry point <cite class='kw'>8</cite> digit

Given a number ending with digit <cite class='kw'>8</cite>, its writing under canonical form is 10 <cite class='kw'>p</cite> + 8. As it is an <cite class='kw even'></cite> number, I have to apply a division by two, which brings a new canonical form of 10 <cite class='kw'>q</cite> + 9 when <cite class='kw'>p</cite> is <cite class='kw odd'></cite> &nbsp;&nbsp;&nbsp; with <cite class='kw'>q</cite> = <cite class='kw'>&#x230a;p / 2&#x230b;</cite> = <cite class='kw'>(p - 1) / 2</cite>&nbsp;&nbsp;&nbsp;<cite class='kw'>&isin; &#x2115; </cite>.  

Now, this computed intermediate results has an ending digit of <cite class='kw'>9</cite> and we have to apply the <cite class='kw'>&omega;</cite> suite calculus, which brings a new canonical form, that is 10 (3 <cite class='kw'>q</cite> + 2) + 8. 

Question: to escape this loop, we must prove that the decimal part <cite class='kw'>d</cite> of the canonical form turns systematically to be even. How to prove that?  
-->




