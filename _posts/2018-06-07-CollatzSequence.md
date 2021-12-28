---
layout: post
title: R - Math - Collatz sequence - part IV
category: category-rmetaverse
summary: overview and discovery of the Collatz sequence
image: images/maths/collatz/cs.png
# comments: true
permalink: rm-r-math-4
---

Find previous posts if you haven't yet read them. [first post](https://neonira.github.io/rm-r-math-1), [second post](https://neonira.github.io/rm-r-math-2), [third post](https://neonira.github.io/rm-r-math-3), .   

## Analysis of <cite class='kw'>cluster 1</cite>

A reminder first.  

<cite class='kw'>cluster 1</cite> is made of numbers with unit digit being part of set <cite class='kw' style='font-size:1.1em;'>S<sub>1</sub></cite> = { <span class='digit digit6'></span>, <span class='digit digit3'></span>, <span class='digit digit0'></span>, <span class='digit digit5'></span> }.

<!--
<span class='digit digit2'></span> 
<cite class='kw'>t</cite>
<cite class='kw even'></cite>
-->

### cluster 1 paths

Reusing results from [second post](math_cs_2) about digit mutation, we can determine all the paths of cluster 1. 

Entry point is unique and is a number ending with digit <span class='digit digit6'></span> , at the notable exception of the starting number that could be any other number of the cluster.  

The typical path is <span class='digit digit6'></span> <cite class='arrow'></cite><span class='digit digit3'></span> <cite class='arrow'></cite> <span class='digit digit0'></span> <cite class='arrow'> (loop possible here)</cite><span class='digit digit5'></span> <cite class='arrow'></cite> <span class='digit digit6'></span>.  

That path is the only one in the cluster. Its length vary considering the loop on <span class='digit digit0'></span> and therefore, the expansion factor will vary also according to this condition.  

The entry condition in cluster 1 has already been demonstrated on [second post](math_cs_2), and <span class='digit digit6'></span> must own an <cite class='kw even'></cite> number of tens to enter the cluster. if not the case, then the <span class='digit digit6'></span> will bring <span class='digit digit8'></span> and switch to cluster 2. 


### cluster 1 expansion factor
<table>
<thead>
<tr style='font-weight:bold'>
<th colspan='5'> <cite class='kw'> &upsilon;<sub>n</sub></cite></th>
</tr>
<tr style='font-weight:bold;font-style:oblique;font-size:.8em'>
<th>n</th>
<th>t</th>
<th>u</th>
<th>computation sequence</th>
<th>expansion factor</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>t is <cite class='kw even'></cite></td>
<td><span class='digit digit6'></span></td>
<td><cite class='kw'>&eta;</cite></td>
<td>1 / 2 = 0.5</td>
</tr>
<tr>
<td>2</td>
<td></td>
<td><span class='digit digit3'></span></td>
<td><cite class='kw'>&omega;</cite></td>
<td>3</td>
</tr>
<tr>
<td>3</td>
<td></td>
<td><span class='digit digit0'></span></td>
<td><cite class='kw'>&eta;</cite></td>
<td>1 / 2<sup>k</sup> &lt;= 0.5 </td>
</tr>
<tr>
<td>4</td>
<td></td>
<td><span class='digit digit5'></span></td>
<td><cite class='kw'>&omega;</cite></td>
<td>3</td>
</tr>
</tbody>
</table>


So, following the path, brings an expansion factor of 9 / 2<sup>k + 1</sup> with k being the number of times we loop on <span class='digit digit0'></span>. Forcibly k <cite class='math_ge'></cite>1.  

if k <cite class='math_ge'></cite>3 then expansion factor becomes a compression factor, meaning the output will be less than the input. You may think to k as the number of 0 on the right of the number. So k <cite class='math_ge'></cite>3 means the number being a multile of 1000.


### Computation analysis
<table>
<thead>
<tr style='font-weight:bold'>
<th>step</th>
<th colspan='9'> <cite class='kw'> &upsilon;<sub>n</sub></cite></th>
</tr>
<tr style='font-weight:bold;font-style:oblique;font-size:.8em'>
<th>n</th>
<th>h</th>
<th>t</th>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
<th>u</th>
<th>rule to apply</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td></td>
<td>t is <cite class='kw even'></cite></td>
<td>0</td><td>2</td><td>4</td><td>6</td><td>8</td>
<td><span class='digit digit6'></span></td>
<td><cite class='kw'>&eta;</cite></td>
</tr>
<tr>
<td>2</td>
<td> h - 1 if t = 0</td>
<td> </td>
<td>5</td><td>1</td><td>2</td><td>3</td><td>4</td>
<td><span class='digit digit3'></span></td>
<td><cite class='kw'>&omega;</cite></td>
</tr>
<tr>
<td>3</td>
<td> h + 1 if t = 3, 4 or 5</td>
<td></td>
<td>6<br>k = 2</td><td>4<br>k = 3</td><td>7<br>k = 1</td><td>0<br>k = 3</td><td>3<br>k = 1</td>
<td><span class='digit digit0'></span></td>
<td><cite class='kw'>&eta;</cite></td>
</tr>
<tr>
<td>4</td>
<td></td>
<td></td>
<td>1</td><td>0</td><td>3</td><td>2</td><td>1</td>
<td><span class='digit digit5'></span></td>
<td><cite class='kw'>&omega;</cite></td>
</tr>

<tr>
<td>5</td>
<td>h + 1 if t = 3 or 4</td>
<td></td>
<td>4</td><td>1</td><td>0</td><td>7</td><td>4</td>
<td><span class='digit digit6'></span></td>
<td><cite class='kw'>&eta;</cite></td>
</tr>
</tbody>
</table>

Read vertically, as cases of tens are shown vertically.  
So, let's take a number that ends with digit <span class='digit digit0'></span>. Its canonical form is 10 <cite class='kw'>t</cite> + 0.  

If <cite class='kw'>t</cite> is <cite class='kw even'></cite>, <cite class='kw'>t</cite> = 2<cite class='kw'>p</cite> this reduces to 5 <cite class='kw'>p</cite> + 0, applying <cite class='kw'>&eta;</cite> two times. Now, if <cite class='kw'>p</cite> is <cite class='kw even'></cite> a further reduction can be applied, and this will happen as long as <cite class='kw'>p</cite> / 2 is <cite class='kw even'></cite>. Let's put <cite class='kw'>e</cite> this number of times, starting from <cite class='kw'>t</cite> input, the total number of times applying <cite class='kw'>&eta;</cite> is therefore 1 + <cite class='kw'>e</cite> with <cite class='kw'>e</cite> <cite class='math_ge'></cite> 1.  <cite class='refeq'>a</cite>  

If <cite class='kw'>t</cite> is <cite class='kw odd'></cite>, <cite class='kw'>t</cite> = 2<cite class='kw'>p</cite> + 1, this reduces to 5 (2<cite class='kw'>p</cite>+ 1) + 0. applying <cite class='kw'>&eta;</cite> one time. <cite class='refeq'>b</cite>  

Note that if a number ends with <cite class='kw'>d</cite> digits <span class='digit digit0'></span>, then the number of times <cite class='kw'>&eta;</cite> will be applied is <cite class='kw'>d</cite>. 

### Expansion factor 

So the expansion factor turns to be taken from set { 9 / 2<sup>k</sup> with <cite class='kw'>k</cite> = 2 when tens of <span class='digit digit0'></span> digit are <cite class='kw odd'></cite>, and <cite class='kw'>k</cite> = 2 + <cite class='kw'>e</cite> with <cite class='kw'>e</cite> being the number of times those tens can be divided by 2 staying <cite class='kw even'></cite>}.  

This expansion factor, is really an expansion factor when tens of <span class='digit digit0'></span> digit are <cite class='kw odd'></cite> or when <cite class='kw'>e</cite> <cite class='math_le'></cite> 2. Otherwise, the expansion factor is a compression factor, meaning that the output of cluster 1 will be in this case a number less than the input number. 

#### Expansion factor pattern

Let's consider input number 13. Applying <cite class='kw'>&omega;</cite>, it brings 40. Applying <cite class='kw'>&eta;</cite> brings successively 40 <cite class='arrow'></cite> 20 <cite class='arrow'></cite> 10 <cite class='arrow'></cite> 5. So <cite class='kw'>e</cite> = 3, and the reduction factor applied is 9 / 16. 

I will show that the expansion factor follows a clearly defined pattern. 

<cite class='kw'> &omega;<sub>n + 1</sub></cite> = 3 <cite class='kw'> &omega;<sub>n</sub></cite> + 1 &nbsp;&nbsp;&nbsp; by definition

<cite class='kw'> &omega;<sub>n + 1</sub></cite> =  3 (100 <cite class='kw'>h</cite> + 10 <cite class='kw'>t</cite> + 3) + 1 = 100 <cite class='kw'>3h</cite> + 10 <cite class='kw'>3t</cite> + 10 = 100 <cite class='kw'>3h</cite> + 10 (<cite class='kw'>3t</cite> + 1) + 0

Therefore, input number has <cite class='kw'>t</cite> tens, and output number has 3<cite class='kw'>t</cite> + 1 tens. Or input number tens have to be taken among { 1, 3, 5, 7, 9 }, leading to following table. 

<table>
<thead>
<tr>
<th>input digit <span class='digit digit3'></span></th>
<th colspan='2'>output digit <span class='digit digit0'></span></th>
<th>minimum <cite class='kw'>e</cite></th>
</tr>
<tr>
<th>input tens </th>
<th>output tens</th>
<th>output hundreds</th>
<th> </th>
</tr>
</thead>
<tbody>
<tr><td>1</td><td>4</td><td></td><td>3</td></tr>
<tr><td>3</td><td>0</td><td>+1</td><td>2</td></tr>
<tr><td>5</td><td>6</td><td>+1</td><td>2</td></tr>
<tr><td>7</td><td>2</td><td>+2</td><td>2</td></tr>
<tr><td>9</td><td>8</td><td>+2</td><td>5</td></tr>
</tbody>
</table>

So what's a surprise! All tens digits of output numbers turns to be <cite class='kw even'></cite>, and their respective expansion factors are shown on the table. Following table expresses the final and definitive expansion factors of cluster 1. 

<table>
<thead>
<tr>
<th>input digit <span class='digit digit3'></span></th>
<th colspan='2'>cluster 1 impact</th>
</tr>
<tr>
<th>input tens</th>
<th>minimum factor</th>
<th>effect</th>
</tr>
</thead>
<tbody>
<tr><td>1</td><td>9 / 16 = 0.5625 </td><td>reduction</td></tr>
<tr><td>3</td><td>9 / 8 = 1.125</td><td>expansion</td></tr>
<tr><td>5</td><td>9 / 8 = 1.125</td><td>expansion</td></tr>
<tr><td>7</td><td>9 / 8 = 1.125</td><td>expansion</td></tr>
<tr><td>9</td><td>9 / 64 = 0.140625</td><td>reduction</td></tr>
</tbody>
</table>








