---
layout: post
title: R - Offensive Programming in action (part II)
category: rmetaverse
summary: What about adding semantic understanding to R, based on conventions.
image: images/op/op-hexsticker-vertical-transparent.png
# comments: true
permalink: rm-r-op-2
---

Many of us are using R in a way or another and we all have to deal with R intrinsics and sometimes R weirdness.

Standard R way
==============

Base package, append function
-----------------------------

Let's look at a first example, using the very useful **append** function from base R.

The function signature is **function (x, values, after = length(x))**. And here, weirdness starts with guessing what are **x**, **values** and **after**?

As often **(always?)**, you will end-up reading the R documentation related to **append** to understand what are the meaning of each parameter, what are their respective types, polymorphic or not, and what are the allowed values.

Generally parameter description in R documentation provides some good hints on intent for each parameter. Far less true for knowing the expected type.

Knowing all of this, you will very probably get to the guess and trial on an R interactive session, as the following sample

``` r
v <- 1:9

append(v, 97, after = FALSE)
```

    ##  [1] 97  1  2  3  4  5  6  7  8  9

``` r
append(v, 97, after = TRUE) # won't provide the result you have in mind
```

    ##  [1]  1 97  2  3  4  5  6  7  8  9

``` r
append(v, 97)
```

    ##  [1]  1  2  3  4  5  6  7  8  9 97

``` r
append(v, 97, after = 5.4) # works! 
```

    ## [1]  1  2  3  4  5 97  6  7  8

``` r
append(v, 97, after = Inf) # works! 
```

    ##  [1]  1  2  3  4  5  6  7  8  9 97

``` r
tryCatch(append(v, 97, after = NA), error = function(e) print(e)) # fails
```

    ## <simpleError in if (!after) c(values, x) else if (after >= lengx) c(x, values) else c(x[1L:after],     values, x[(after + 1L):lengx]): missing value where TRUE/FALSE needed>

``` r
tryCatch(append(v, 97, after = -1), error = function(e) print(e)) # fails
```

    ## <simpleError in x[1L:after]: only 0's may be mixed with negative subscripts>

``` r
append(v, 91:99)
```

    ##  [1]  1  2  3  4  5  6  7  8  9 91 92 93 94 95 96 97 98 99

``` r
append(v, 91:99, after = 0)
```

    ##  [1] 91 92 93 94 95 96 97 98 99  1  2  3  4  5  6  7  8  9

``` r
append(v, letters[1:7], c(3, 5, 2, 1, 4))
```

    ## Warning in if (!after) c(values, x) else if (after >= lengx) c(x, values)
    ## else c(x[1L:after], : the condition has length > 1 and only the first
    ## element will be used

    ## Warning in if (after >= lengx) c(x, values) else c(x[1L:after], values, :
    ## the condition has length > 1 and only the first element will be used

    ## Warning in 1L:after: numerical expression has 5 elements: only the first
    ## used

    ## Warning in (after + 1L):lengx: numerical expression has 5 elements: only
    ## the first used

    ##  [1] "1" "2" "3" "a" "b" "c" "d" "e" "f" "g" "4" "5" "6" "7" "8" "9"

``` r
append(v, list(96, 97, 98)) # what is the output of appending a list to a vector?
```

    ## [[1]]
    ## [1] 1
    ## 
    ## [[2]]
    ## [1] 2
    ## 
    ## [[3]]
    ## [1] 3
    ## 
    ## [[4]]
    ## [1] 4
    ## 
    ## [[5]]
    ## [1] 5
    ## 
    ## [[6]]
    ## [1] 6
    ## 
    ## [[7]]
    ## [1] 7
    ## 
    ## [[8]]
    ## [1] 8
    ## 
    ## [[9]]
    ## [1] 9
    ## 
    ## [[10]]
    ## [1] 96
    ## 
    ## [[11]]
    ## [1] 97
    ## 
    ## [[12]]
    ## [1] 98

``` r
append(expression({z <- 3; d <- x + y + z}), expression({x <- 1; y <- 2}), after = FALSE)
```

    ## expression({
    ##     x <- 1
    ##     y <- 2
    ## }, {
    ##     z <- 3
    ##     d <- x + y + z
    ## })

Not even considering weird cases where you want to insert values in the first argument vector that changes its nature from standard vector to long vector, this function appears to be complex to use, and faces following issues

1.  arguments are dumb. You must read the documentation to know what they mean and embody.
2.  argument arities are unclear
3.  argument types are unclear
4.  result value is nearly unforeseeable, as it result of internal coercition and internal type conversions
5.  result type is difficult to predict. It follows type concatenation rules
6.  append function does in reality append, prepend and insert at functions

Base R, isTRUE function
-----------------------

A second example on base package function **isTRUE**.

``` r
isTRUE
```

    ## function (x) 
    ## is.logical(x) && length(x) == 1L && !is.na(x) && x
    ## <bytecode: 0x5610b8d39d98>
    ## <environment: namespace:base>

``` r
isTRUE(0)
```

    ## [1] FALSE

``` r
isFALSE(0) # result is not what you probably expect 
```

    ## [1] FALSE

``` r
isTRUE(Inf) # Call Spinoza, I've got an headache. 
```

    ## [1] FALSE

``` r
isTRUE(NaN)
```

    ## [1] FALSE

``` r
isTRUE(NA_complex_)
```

    ## [1] FALSE

``` r
isTRUE(rep(TRUE, 10)) # result is not what you probably expect 
```

    ## [1] FALSE

Here again, very difficult to guess arguments and results. I could easily consider any function of R, and probability for interpretation weirdness about parameters is high. Quality of documentation helps but remains insufficient to ease confident guessing of parameter types, length and values.

Offensive programming way
=========================

If you are trying to figure out how to reduce this weirdness, then, it's time to consider using at a much larger scale offensive programming scheme.

Offensive programming is based on semantic naming. One of its virtues is to provide much more intuitive argument naming. Applied to **append**, the accurate signature corresponding to the base R function is **function(stockValues\_, valuesToInsert\_, afterIndex\_ui\_1 = length(x))**.

Function **code remains the same**. It has just to be aligned with the new argument names. No other change has to be considered.

What are the benefits of this semantic naming?
----------------------------------------------

1.  arguments **stockValues\_** and **valuesToInsert\_** are both ending with underscore. They are polymorphic arguments, meaning, arguments that can take several types. As this is mentioned in their named, and as you now know it, your awareness about type conversion is increased. In particular, composing two different types should raise your attention.
2.  argument **afterIndex\_ui\_1** brings even more information. It means one and only one value is expected and it has to be an unsigned integer ('ui').

Not only signature allows you to use immediately the function, without reading its documentation, but it also provides key information about type and length to ease its usage, and prevents some misuses (negatives indexes, multiple indexes, ...)

Indeed, to be completely an offensive programming instrumented function, function return type and test case instrumentation should be also provided. This would bring us too far for the moment, and will be presented in some other coming posts.

What does it change?
--------------------

From a global perspective, the parameter type and length scopes are now specified by the applied semantic naming scheme. This brings following benefits at a function scope

1.  no need to verify the types
2.  no need to verify the length

Thus code implementation is reduced from that burden. Value verification may still stand, depending of the types you use. When using specialized types (common ones or your owns), there is no more need to verify values legality at the function entry.

Know the basics of semantic naming
----------------------------------

### How to turn any function parameter into a semantic name?

A semantic name complies with following pattern: **&lt;variableName&gt;\_&lt;typeSuffix&gt;\_&lt;lengthSpecification&gt;**

Type suffix and length specification parts are optional.

If your type is polymorphic, its semantic name must end by a single underscore.

### What are the most common type suffixes?

Let's start by standard R types

| type suffix | meaning   |
|:------------|:----------|
| l           | list      |
| lo          | logical   |
| i           | integer   |
| d           | double    |
| n           | numeric   |
| c           | complex   |
| ch          | character |
| r           | raw       |
| f           | function  |
| fa          | factor    |

Some very convenient types, specialization of some base types

| type suffix | meaning                                              |
|:------------|:-----------------------------------------------------|
| b           | boolean, either TRUE or FALSE, never NA\_logical\_   |
| s           | string, never NA\_Character\_                        |
| ui or pi    | positive integer                                     |
| ni          | negative integer                                     |
| r or rm     | real math, double, never NA\_double nor Inf nor -Inf |
| pr          | positive real math                                   |
| nr          | negative real math                                   |
| cm          | complex math, never NA\_complex nor Inf nor -Inf     |

To get the full list of registered type suffixes, simply use

``` r
library('wyz.code.offensiveProgramming')
retrieveFactory()$getRecordedTypes()
```

You are invited to register your own type into the function parameter type factory whenever you need. Doing so, allows you to introduce your own type suffixes, and use them immediately. This is a purely declarative approach that do not requires your types to be already implemented. That way, you can use suffixes immediately in your code.

### Length specification at a glance

I will use *myIndex\_pi* as an example name for a parameter function, throughout this paragraph.

When you know the constraints of length on one parameter, you may specify them, according to following table

| length constraint   | what to do                 |                                    |
|:--------------------|:---------------------------|:-----------------------------------|
| exact length        | use length figure          | myIndex\_pi\_7 (length 7)          |
| exact length or one | use suffix n               | myIndex\_pi\_7n (length 7 or 1)    |
| less than           | use suffix l               | myIndex\_pi\_7l (length &lt;= 7)   |
| more than           | use suffix m               | myIndex\_pi\_7m (length &gt;= 7)   |
| unknown             | do not specify length part | myIndex\_pi (unconstrained length) |

### Test your understanding

Now, you know all the basic, and are ready to put that in action.

What is the parameter name

1.  for a character vector of length 5?
2.  for a boolean vector of length 1 or more?
3.  for a function or function name of length 3
4.  for a list or data.table of unconstrained length
5.  for a matrix of real math?

Possible answers

1.  names\_s\_5 or names\_ch\_5 depending of possibility of NA in content
2.  myFlag\_b\_1m
3.  functionOrFunctionName\_3\_ *(final underscore mandatory to notify a polymorphic type)*
4.  listOrDataTable\_ *(idem)*
5.  no way currently - you should create your own type and register it to manage such a case

To conclude
===========

We have seen, that at the price of a few extraneous characters for each function parameter, and by adopting offensive programming approach, we may reduce several sources of weirdness in R

1.  argument types are explicit, or explicitly polymorphic
2.  argument lengths are either explicitly stated, or remains unstated,
3.  argument verification tied to types and length are now obsoletes. You should not implement them anymore into your R functions, unless dealing with a polymorphic type.

Registering your own type suffixes is a way to write once and only once the verification code, and to reuse it on demand or programmatically. This simplifies your R function implementation, increases your productivity, while staying fully under control. To achieve this, watch for next post! We'll learn how to put offensive programming in action.
