---
title: Collatz Sequence - part 1
hidden: false
categories: mathematics EN
tags: mathematics R computing 
author: neonira
permalink: math_cs_1
output:
  html_document:
    number_sections: true
---
[Collatz sequence](https://en.wikipedia.org/wiki/Collatz_conjecture) is a well known suite mathematical suite, remaining unproved as far as I know. 
Let's play with it and discover some of its secrets.  

To discover its behavior, we stop whenever we reach 1 as input, otherwise depending on parity of &upsilon;<sub>n</sub>, we apply  
![collatz definition](/images/maths/collatz/cs.png)  
Let's name 3&upsilon;<sub>n + 1</sub> the <cite class='kw'>ODD</cite> rule, and the other the <cite class='kw'>EVEN</cite> rule.  

## Notation convention used in this document

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
**Result 1.1**: The conjecture is true for all <cite class='kw'>1</cite> digit numbers. 
</span>

<span class='tip'> 
**Result 1.2**: Each number <cite class='kw'>2<sup>k</sup></cite> with <cite class='kw'>k &#8805; 1</cite> will converge to the final value <cite class='kw'>1</cite> in <cite class='kw'>k</cite> steps. 
</span>

<span class='tip'> 
**Result 1.3**: Each number <cite class='kw'>20q</cite> with <cite class='kw'>q &isin; &#x2115;<sup>*</sup></cite> will converge to the final value <cite class='kw'>1</cite> in <cite class='kw'>q + 6</cite> steps. 
</span>

<span class='do'> 
**LESSON LEARNT 1.1** The number of steps for an odd number to be reduced to<cite class='kw'>1</cite>, is irregular. For example, <cite class='kw'>5</cite> took <cite class='kw'>6</cite> steps, whereas <cite class='kw'>3</cite> took <cite class='kw'>8</cite>. 
In the same time, a higher dimension of the input will bring a higher number of steps to converge to <cite class='kw'>1</cite>.   
</span>

<span class='do'> 
**LESSON LEARNT 1.2**: When proceeding to computation, we could end up earlier the processing, whenever we reached a number that is less than the starting input. 
For example, consider starting number <cite class='kw'>9</cite>. Instead of doing the <cite class='kw'>19</cite> computations required, we could have stopped at the first number in the suite
 below the starting number <cite class='kw'>9</cite>, id est <cite class='kw'>7</cite> that 
appears in third place. 
</span>

## Understanding the suite internal behavior and processing paths

### Basic understanding

The processing path is quite simple here. No shortcut, rigorous application of the <cite class='kw'>&upsilon;<sub>n + 1</sub></cite> suite rules.

![basic understanding](/images/maths/collatz/algo1.png)

### A little bit more subtle understanding

Whenever we take an odd number multiply it by <cite class='kw'>3</cite> and add <cite class='kw'>1</cite>, we end up with an even number. So in fact, each time we apply odd transformation, an even transformation will follow. 

![more subtle understanding](/images/maths/collatz/algo2.png)


This leads us to some insights. First, analyzing the possible paths on this graph, we have in fact only two possible loops. The first one will be named <cite class='kw'>TIC</cite> and is given by <cite class='kw'>(OE)+</cite>, the second one will be named <cite class='kw'>TAC</cite> and is given by <cite class='kw'>(OE{2,})</cite>. Syntax used here complies with PERL 5 regular expression syntax. This means that whenever we encounter an odd number we will apply either <u>once and only once</u> a parity condition, or <u>several times</u>.  

Let's see the consequences of this. 
#### TAC case analysis

Here we alternate **regularly** <cite class='kw'>ODD</cite> and <cite class='kw'>EVEN</cite> suite rules for an unknown number of steps.

![TAC definition](/images/maths/collatz/cs2.png)  

<span class='warn'> 
**INSIGHT 2.1**: The <cite class='kw'>TAC</cite> suite is naturally diverging to &#x221e; as we multiple each time by <cite class='kw'> 3 / 2</cite>.
</span>

<span class='do'> 
**LESSON LEARNT 2.1**: The <cite class='kw'>TAC</cite> suite, whenever appearing in the computation, brings a natural integer as result, that will be greater than its input. So, it is an expansion factor. 
</span>


#### TIC case analysis

Here we do not alternate **regularly** <cite class='kw'>ODD</cite> and <cite class='kw'>EVEN</cite> suite rules. 
Instead we apply first and once and only once the <cite class='kw'>ODD</cite> rule, and then apply at <cite class='kw'>k</cite> times the <cite class='kw'>EVEN</cite> rule, with <cite class='kw'> k &#8805;  2</cite>.   

![TIC definition](/images/maths/collatz/cs3.png)  
 

<span class='warn'> 
**INSIGHT 3.1**: The <cite class='kw'>TIC</cite> suite is converging to <cite class='kw'>0</cite> with <cite class='kw'>k &rarr; &#x221e;</cite>. This means that the number we compute, will be lesser than the number we used as input.
</span>

<span class='do'> 
**LESSON LEARNT 3.1**: The <cite class='kw'>TIC</cite> suite, whenever appearing in the computation, brings a natural integer as result, that will be smaller than its input. So, it is a reduction factor. 
</span>

#### Digit mutation analysis
It appears that Collatz sequence turns digits in a very strange way, due to its definition. All results can be summarize at a digit level with following figure. 

![digit sequence path](/images/maths/collatz/digit-sequence.png)

This graphs shows that the digit paths have well established cycles, and that we can consider 3 different clusters. First cluster is based on numbers ending with a digit <cite class='kw'>6</cite>. That's also the cluster of numbers that are multiples of <cite class='kw'>10</cite>. 
Second cluster is based on source numbers ending with a digit <cite class='kw'>4</cite>, and the third cluster based on numbers ending with a digit <cite class='kw'>8</cite>.

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

So, if we want to prove the conjecture, then we just have to prove it for any number with digit <cite class='kw'>4</cite> or <cite class='kw'>6</cite> or <cite class='kw'>8</cite> that are the entry points of each cluster. We'll try this in second post to come.  


