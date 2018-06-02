---
title: Collatz Sequence - part 1
hidden: false
categories: mathematics
tags: mathematics R computing 
author: neonira
permalink: math_cs_1
output:
  html_document:
    number_sections: true
---
[Collatz sequence](https://en.wikipedia.org/wiki/Collatz_conjecture) is a well known suite mathematical suite, remaining unproved as far as I know. 
Let's play with it and discover some of its secrets.  

To discover its behavior, we stop whenever we reach 1 as input, otherwise depending on parity of <span>$$ u_n $$</span>, we apply  
<span>$$ u_{n + 1} = 3u_n + 1  $$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for an odd number - let's name it <cite class='kw'>ODD</cite> rule.</span>  
<span>$$ u_{n + 1} = {u_n \over 2}$$ &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for an even number - let's name it <cite class='kw'>EVEN</cite> rule. </span>  


##### Notation convention used in this document

All lowercase ASCII letters stands for natural integers.  
The 'o' always means an odd integer.  
The 'e' always means an even integer.  

## Some trials ... 

Let's start our analysis by playing with some elementary numbers, to get more familiar with the Collatz sequence generation suite. 

```r
#First number shown on each line is the starting number of the sequence
#Number in bracket is the number of steps to reach 1
> sapply(2:9, cn$getCollatzSequence)
2 : 1 [1] 
3 : 10 5 16 8 4 2 1 [7] 
4 : 2 1 [2] 
5 : 16 8 4 2 1 [5] 
6 : 3 10 5 16 8 4 2 1 [8] 
7 : 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1 [16] 
8 : 4 2 1 [3] 
9 : 28 14 7 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1 [19] 
```

<span class='tip'> 
**Result 1.1**: The conjecture is true for all <span> $$ 1 $$</span> digit numbers. 
</span>

<span class='tip'> 
**Result 1.2**: Each number <span>$$ 2^k $$</span> with <span>$$ k \ge 1 $$</span> will converge to the final value <span> $$ 1 $$</span> in <span> $$ k $$</span> steps. 
</span>

<span class='tip'> 
**Result 1.3**: Each number <span>$$ 20q $$</span> with <span>$$ q \in N^* $$ </span> will converge to the final value <span> $$ 1 $$</span> in <span> $$ q + 6 $$</span> steps. 
</span>

<span class='do'> 
**LESSON LEARNT 1.1** The number of steps for an odd number to be reduced to <span> $$ 1 $$</span>, is irregular. For example, <span> $$ 5 $$</span> took <span> $$ 6 $$</span> steps, whereas <span> $$ 3 $$</span> took <span> $$ 8 $$</span>. 
In the same time, a higher dimension of the input will bring a higher number of steps to converge to <span> $$ 1 $$</span>.   
</span>

<span class='do'> 
**LESSON LEARNT 1.2**: When proceeding to computation, we could end up earlier the processing, whenever we reached a number that is less than the starting input. 
For example, consider starting number <span> $$ 9 $$</span>. Instead of doing the 19 computations required, we could have stopped at the first number in the suite
 below the starting number <span> $$ 9 $$</span>, id est <span> $$ 7 $$</span> that 
appears in third place. 
</span>

## Understanding the suite internal behavior and processing paths

### Basic understanding

The processing path is quite simple here. No shortcut, rigorous application of the <span>$$ u_{n + 1} $$</span>suite rules.

![basic understanding](/images/maths/collatz/algo1.png)

### A little bit more subtle understanding

Whenever we take an odd number multiply it by <span> $$ 3 $$</span> and add <span> $$ 1 $$</span>, we end up with an even number. So in fact, each time we apply odd transformation, an even transformation will follow. 

![more subtle understanding](/images/maths/collatz/algo2.png)


This leads us to some insights. First, analyzing the possible paths on this graph, we have in fact only two possible loops. The first one will be named <cite class='kw'>TIC</cite> and is given by <span> $$ (OE)+$$</span>, the second one will be named <cite class='kw'>TAC</cite> and is given by<span> $$ (OE{2,})$$</span>. Syntax used here complies with PERL 5 regular expression syntax. This means that whenever we encounter an odd number we will apply either <u>once and only once</u> a parity condition, or <u>several times</u>.  

Let's see the consequences of this. 
#### TAC case analysis

Here we alternate **regularly** <cite class='kw'>ODD</cite> and <cite class='kw'>EVEN</cite> suite rules for an unknown number of steps.

<span>$$ u_{n + 2} = {3u_n + 1  \over 2} $$</span>

<span class='warn'> 
**INSIGHT 2.1**: The <cite class='kw'>TAC</cite> suite is naturally diverging to &#x221e; as we multiple each time by <span> $$ { 3 \over 2 } $$</span>
</span>

<span class='warn'> 
**INSIGHT 2.2**: Applying <span> $$ k $$</span> times the <cite class='kw'>TAC</cite> suite,  XXX
</span>

<span class='do'> 
**LESSON LEARNT 2.1**: The <cite class='kw'>TAC</cite> suite, whenever appearing in the computation, brings a natural integer as result, that will be greater than its input. So, it is an expansion factor. 
</span>


#### TIC case analysis

Here we do not alternate **regularly** <cite class='kw'>ODD</cite> and <cite class='kw'>EVEN</cite> suite rules. 
Instead we apply first and once and only once the <cite class='kw'>ODD</cite> rule, and then apply at least two times the <cite class='kw'>EVEN</cite> rule.   


<span>$$ u_{n + k} = {3u_n + 1  \over 2^k} $$ with $$ k \ge 2 $$ and where $$ k $$ is the number of times we apply the <cite class='kw'>EVEN</cite> suite rule</span>.

<span class='warn'> 
**INSIGHT 3.1**: The <cite class='kw'>TIC</cite> suite is converging to <span> $$ 0 $$</span> with <span> $$ k $$</span> trending to &#x221e;. This means that the number we compute, will be lesser than the number we used as input.
</span>

<span class='do'> 
**LESSON LEARNT 3.1**: The <cite class='kw'>TIC</cite> suite, whenever appearing in the computation, brings a natural integer as result, that will be smaller than its input. So, it is a reduction factor. 
</span>

#### Digit mutation analysis
It appears that Collatz sequence turns digits in a very strange way, due to its definition. All results can be summarize at a digit level with following figure. 

![digit sequence path](/images/maths/collatz/digit-sequence.png)

This graphs shows that the digit paths have well established cycles, and that we can consider 3 different clusters. First cluster is based on source numbers that are multiples of <span> $$ 10 $$</span>. 
Second cluster is based on source numbers ending with a digit <span> $$ 4 $$</span>, and the third cluster based on numbers ending with a digit <span> $$ 8 $$</span>.

<span class='warn'> 
**INSIGHT 4.1**: Note that to enter <cite class='kw'>cluster 2</cite> you must have a digit division with tens being even and to enter <cite class='kw'>cluster 1</cite> or <cite class='kw'>cluster 1</cite> you must have a digit division with tens being odd. 
</span>

<span class='warn'> 
**INSIGHT 4.2**: Note that each cluster have only one entry point and one exit point. Entry and exit point are unique for <cite class='kw'>cluster 1</cite> and <cite class='kw'>cluster 3</cite> and are distinct for <cite class='kw'>cluster 2</cite>.
</span>

<span class='warn'> 
**INSIGHT 4.3**: Each digit belongs to one and only one cluster. 
</span>


## Conclusion of part 1

So, if we want to prove the conjecture, then we just have to prove it for any number with digit <span> $$ 4 $$</span> or <span> $$ 6 $$</span> or <span> $$ 8 $$</span> that are the entry points of each cluster. We'll try this in second post to come.  


