---
layout: post
title: Main issues when switching from R to Python and vice versa
category: category-rmetaverse
summary: impediments on the road of managing two code bases ... 
image: images/books/amok.jpg
# comments: true
permalink: pl-cmp-23
---

<link rel="stylesheet" href="/assets/css/my-styles.css">

A lot have been written about R and Python ecosystems differences and when to use one or the other. A good reference to be browsed is [IBM - Python vs. R: What’s the Difference?](https://www.ibm.com/cloud/blog/python-vs-r) 

I want to address the difference from a much more pragmatical point of view and not from a stratospheric one. From a developer point of view, whom could use both languages, what are the main difficulties and issues faced when having to deal with two code bases, one in R, the other in Python?


# Ecosystem mastery

Mastering the R and the Python ecosystems is tricky. It requires a lot of efforts and a strong memory as package names, versions and features are simply not matching at all. 

Very concretely, this involves knowing the names and versions of packages and functions, their invocation parameters and their potential exceptions and limits. Much easier said than done, especially when you have to deal with several tens of them for each code base.

Both languages comes with several versions. Managing language version updates might bring strong impacts. Much more for Python indeed, as there exists a Pythonic way that aims to provide the right way of coding for a given goal. Main difficulty for the designer here, is that the Pythonic way changes a lot from version to version of Python. You cannot apply the same Pythonic way under Python 2.X or Python 3.X, as many features have been introduced to the core language, that is still evolving quite a lot. From a stability point of view, R evolves gently at core and deeply at edges with many new packages each week, while Python tends to follow the opposite trend: deep changes at core and less changes at edges. 


# Object oriented design complexity

Using R language, you face a choice of several OOP flavors: S3, S4, RC, R6 and even the recent R7 paradigm are available to choose from. This requires a deep knowledge to select wisely the best way. 

Refer to [Hadley Wickham - Advanced R](https://adv-r.hadley.nz/) and to [R-bloggers - R7](https://www.r-bloggers.com/2022/07/comments-on-the-new-r-oop-system-r7/) to know more about each of them. 

At the opposite, Python offers a more readable way of creating class, as this is one of its core features. Refer to [Python class](https://docs.python.org/3/reference/compound_stmts.html#class) to get deeper insight about it. Indeed, having a closer look, you will understand that there exists several class specializations and decorations that will impact class behavior. Mastering all of them requires time and is not so intuitive. 


# Data structures versatility

| data structure name | core<br/>R | core Python | comment
|-----------------------:|:-----:|:-------:|:------------------------------------------|
| vector or array | <cite style='color:forestGreen'>&#10004;</cite> | <cite style='color:forestGreen'>&#10004;</cite> |
| list  | <cite style='color:forestGreen'>&#10004;</cite> | <cite style='color:forestGreen'>&#10004;</cite> | 
| matrix  | <cite style='color:forestGreen'>&#10004;</cite> | <cite style='color:darkRed'>&#10004;</cite> | i.e. a multi-dimensional array in Python
| data frame  | <cite style='color:forestGreen'>&#10004;</cite> | <cite style='color:darkRed'>&#10004;</cite> | requires a dedicated module in Python
| tuple | <cite style='color:darkRed'>&#10006;</cite> | <cite style='color:forestGreen'>&#10004;</cite> | immutable list in Python
| set   | <cite style='color:darkRed'>&#10006;</cite> | <cite style='color:forestGreen'>&#10004;</cite> | results generally from functional operation in R
| dictionary | <cite style='color:darkRed'>&#10006;</cite> | <cite style='color:forestGreen'>&#10004;</cite> | i.e. a named list in R

As core data structure are quite different for these two languages, programming in one or the other will require some agility to exploit the best of breed provided by each one. 

One main difference, whatever the data structure, its slicing is quite generically addressable using the same syntax in each language, but unfortunately slicing syntax is language dependent and clearly incompatible between R and Python. In R, negative indexes are use to remove entries while in Python they are use to start from the end of the considered data structure. Dealing with this is error prone and requires recurring concentration efforts to avoid the from now on known traps. 

Second difference, worth to remember, is array indexes do not start at same value: 0 for Python, 1 for R. This is of some importance when porting algorithm from one language to another. 

# Programming behavior

Programming using each of them is quite similar although some key differences exists. Here are the main ones

1. Control structures exists in both languages but do not share the exact same syntax. 
1. R brings a 3 state Boolean algebra (TRUE, FALSE, NA), while Python sticks to a 2 state one (True, False). Note that typography of the Boolean values differs. 
1. R owns raw type at core and there is no such equivalent type in Python
1. R complex numbers are available at core for both languages. Indeed mathematical functions are natively available in R, not in Python (see below sqrt example)
1. Exceptions exist in both languages but each of them remains specific to its ecosystem. This requires some hard work to adapt code base from one language to the other. 
1. Python 3.10 and ulterior versions brings some new features about meta programming. I found them still messy and confusing comparing native meta-programming features available in R. In particular, ability to build at run time functions, or to change functions signatures or function body, is particularly easy in R and still quite cumbersome using Python 3.10 or higher. 
1. Each language brings its own way to deal with code documentation. Both are reliable although completely different. This may require some hard and long work when porting a code base from one language to another
1. Remember that the same function or class name might embody two very different things in each language. Moreover, parameters to be used will very probably be named differently and might not accept same value types, same value range, and might even do not have same default values. Portage is hence quite difficult as these impact are extremely hard to forecast. 

# Syntaxic sugar

Common features to both languages worth to notice:

1. Comments. No work to be achieved as both languages share the same comment approach in code, both introduced by a sharp sign. I speak here about code comments only and not of code documentation
1. ability to return functions from functions, and to use functions as arguments. Both languages perform well on these topics and for each of them, functions are easy to define and use. 

Python come with some mechanism unknown from R, here is a short and not exhaustive list

1. place holder for dummy variables, named '_' in Python,
1. possible multiple assignments from deconstruction of data structure in one line
1. function and class annotations are common in Python, and this reduces code volume and eases code unification. Equivalent can be quite easily coded in R by composing functions but this requires extraneous implementation for the developer. 
1. the Python <cite style='font-weight:bold'>match</cite> operator seems superior to the <cite style='font-weight:bold'>switch</cite> or R
1. ability to produce pure executable for a given platform. I do not know any equivalence of this feature in R world. 


R comes with following mechanism that requires some work in Python 

1. functions can return versatile values. A same function in R can return a data frame, an integer, or a complex number depending of the executed code branch. Achieving this with Python requires latest versions - from 3.10 to latest - and to declare specifically in the code the expected returned types for this function.
1. vectorization is native in R, not in Python. You will need to import a dedicated library - as <cite style='font-weight:bold'>numpy</cite> for example - to achieve this under Python. As this mechanism is not native in Python, recycling rules differ from R. Know it. Refer to [Geek4Geek article](https://www.geeksforgeeks.org/vectorization-in-python/) to know more. 
1. as core types supported by R are different, common functions available in R, might require a library to be matched in Python. For example,  <cite style='font-style:mono'>sqrt(3i)</cite> in R, will compute the expected results. Achieving the same with Python, will require you 
    a. to transpose i in j
    b. to identify a Python library dealing with complex numbers and offering an algorithm to compute square roots according to the original algorithm computed in R as Python Math library sqrt function does not deal with complex number. This issue might sound easy to solve, but will require some time for research, test and verification. 
1. R brings NA for each core type and provides ability to handle it anywhere in the code base. Doing so with Python will require to create some classes to manage neatly the various cases.


# Philosophy

Using R, you will feel very free of the approach. There exists several ways to achieve the result you seek for, and you will have to peak the one that fits your requirements according to performance, reproducibility and to R universe you want to stick to (Core R, Tidyverse, Specific combination).

Using Python, you will have to go the Pythonic way. It comes with a good side, that it drives you efficiently to a result, and with a down side, that it does not give you much attitude to other approaches. 

# Tools

I voluntary kept off from the tools in each ecosystem. Their goal and number may differ according to various constraints you may face. 

For example, when dealing with R code base, I was using [RSTUDIO IDE](https://posit.co/), while when I was dealing with Python code, [visual studio code](https://code.visualstudio.com/) was used. Very difficult to draw any conclusion from this, both are strong, reliable and helpful in achieving greater code base quality. 

Moreover, CI/CD chain were very dissimilar, and this prevents me from drawing any conclusion on it, except that full automation in R ecosystem through [github](https://github.com/) - encompassing package production on many platforms and code coverage - where impressively efficient. 


# Last word

Although not exhaustive, several pain points related to managing two code bases, one in R, one in Python, have been identified and described. Solutions exists and require some hard work to be put in action. 

My return on experience is that it is better to have two teams, each specialized on each language to achieve the work. It will consume less time and energy, as this is a real torture having to think in two similar but deeply different worlds that are R and Python ecosystems. 

