---
layout: post
title: R - CRAN submission REX
category: category-rmetaverse
summary: Return of experience on CRAN package submissions
image: images/cran/cran.jpg
# comments: true
permalink: rm-r-cran-1
---

I submitted my first R packages a few weeks ago, and I believe it's worth
sharing some return on experience, as the **CRAN** submission and acceptance 
processes are much more tricky than they appear at first glance. 

Package preparation and bundles were achieved using **RStudio** as IDE to 
implement code and documentation, and to generate package bundles. I gave attention 
to get to no error, no warning and no note status prior any **CRAN** submission. 


# Package submission process

Package submission process is quite straightforward. It is a fully digital
process, achieved online, that is mainly a sequence of three steps. 

1. Upload your R package source bundle
2. Confirm R package submission
3. Wait for feedback 

## R package source bundle uploading

This is done online through [submission URL](https://cran.r-project.org/submit.html). 
Fill in your name, email address and  select your R package source bundle file to be uploaded. Then submit the form. 

R package submission process will send an email to the provided email address.

This first activity of the submission process us quite simple, works fine, and 
is an easy step to go through. 


# Confirm R package submission

In this received email, click on the confirmation link to confirm your package 
submission. 

This second activity of the submission process is simple and easy. I met no 
issue there. 


# Wait for feedback

This part implies much more hidden work, from the **CRAN** team. It includes both
automated checks and human introspection of your package content. 

Feedback might requires some changes in your package content. So, you will have
to proceed to the required changes, and replay the submission process. 
Unfortunately, the number of replays is nearly unpredictable, even when starting
from a perfectly correct R package bundle (no error, no warning, no note).

This third activity of the submission process is really difficult. First 
difficulty is understanding the required changes and their root cause. Second 
difficulty is proceeding to changes while keeping a high level of integrity in 
your package pieces. Sometimes a small required change will have a humongous 
impact on your code or documentation and you may have to transform your 
approach whenever required. 

From my experience, here are the main pitfalls I faced, and if you plan to 
submit a package to **CRAN**, get acknowledged to them 

## R Package structure 

Main pitfalls I faced came from two sources: The DESCRIPTION file, and the 
folder structure of the R package. 

### DESCRIPTION FILE

This file has been the source of the greatest numbers of changes in my various 
submissions. 

First, version field does not allow for zero led version numbers. Version 0.1.1 
is legal, 1.4.23 is also legal, but version 1.04.023 is not. That's a fact,
I was ignorant about. 

Second, do not write lastnames entirely using upper cased letters. Capitalizing 
last name is sufficient and the expected way by **CRAN**. I stil do not know why, 
but I had to re-submit a package for that reason. 

Third, each time you submit a new release of your R package, you must increase
the version number. The **CRAN** submission process does not allow you to submit
several times the same version, and will flag this as an error. Even if you 
change a single comma, you must change the version number. You may change it, in
anyway you like, up the fix number, the minor number, the major number of any 
combination of them. When taken in the flow of re-submissions, do not forget, to
increase the version number, or get ready for a new submission process run. 

Fourth, description field requires understand-ability. Readers should understand
the purpose and the value of your package by reading it. I had the bad trend to
keep it short. I was wrong. Being explicit and being long is right for this 
field. Use plain English language and be sure to fix all the typos here. Stick 
to known and regular vocabulary. Do not try to be creative here, as it will 
very probably bring you in the aftermath of re-submission. 

Fifth, I encountered some issues with references. If you need to state a 
reference to an **ISBN** or **DOI** for example, syntax to use is described
[CRAN policy](https://cran.r-project.org/submit.html). Main issue here, is that this documentation lacks inspiring 
examples. I ended up guessing the syntax, and generally I guessed wrongly.
To avoid failure, consider following template, __'Refer to chapter {X} of 
{bookName}, {Firstname} {LASTNAME} ({YEAR}, ISBN:{isbn_number})'__, and replace everything between braces (including braces themselves}, by the data for your case. 

### R package folder structure

Main issues came from the use of package folder structure to achieve various
goals, that are not related to R package delivery. In particular, I was used to
store architecture notes, design notes, implementation notes and maintenance 
notes in a dedicated folder under __inst__ folder. That's wrong for at least 
two reasons. First it exposes information that should not. Second, it increases
weight of the R package without adding any value for the package users. 

I get back to a **KISS** strategy and simply removed those folders from the 
delivery.

## R code 

Here I faced two issues, that it is worth to know

First, I used __assign__ to global environment to increase package usability,
and increase user's productivity. Wrong, as this is not allowed by the **CRAN**.
Apparently, assigning to global environment is simply forbidden by their 
acceptance procedure. 

Second issue is a very common one, apparently. Writing files in package 
structure instead of in a temporary folder. Each time, your code, for any
reason, requires to write a file, you must use __tempdir__ for the package to
pass the submission process. It is not allowed to write in the package structure. 
This means, that I had to change the function signatures to take into account a
target folder parameter, which defaults to __tempdir()__, and can be changed by
user whenever and wherever required. 

Note that **CRAN** acceptance does not mean your package code is valid, 
nor useful, nor correct. This is the package author's responsibility to ensure
these qualities, not the **CRAN** team ones. 

## R documentation

I am very familiar with [Writing R extensions](https://cran.r-project.org/doc/manuals/r-release/R-exts.html) 
and about R documentation scheme. So, I expected to have a smooth submission
process, from the documentation point of view. 

I faced two main issues, one with __.Rdoc__ files, the other with vignette files.

### R documentation issues

My main issue was about the usage I did of __\\dontrun__ tag. Human introspection
of the code I submitted, brought change requests on this topic. 

This tag should be used when the processing time implied by the considered part,
exceeds 5 seconds. Change, rince and re-submit. 


### R vignettes issues

Issue what tied to dynamically generated vignettes, which implied previously
presented issue about R code writing into un-allowed places. As this was done,
to achieve incremental trace-ability, with no value for end-users, I simply 
dropped the erroneous vignettes, and kept the useful ones. 

## Process weirdness

### **CRAN** vs **RStudio** 

You have to know that **CRAN** does not know about commercial tool **RStudio**. 

Main consequence of this fact is that **CRAN** checks are not the same as the
checks achieved in **RStudio**, even when passing __--as.cran__ parameter, thus 
leading each of us, to understand two different verification processes: the one
from the **CRAN**, that involves human inspection, and the one from **RStudio**
tools, that is fully automated. 

It took me some time to figure out why I faced no issue using **RStudio** while
**CRAN** team, in a fair and meaningful way, was requiring changes to my 
packages. All issues I encountered, except the assignment one, have not been
detected by the **RStudio** tools. 

Exchanges with **CRAN** team members brought some light. Human inspection of 
the package content aims to ensure understand-ability, to achieve a kind of 
integrity accros packages, and to filter out most common R code and R 
documentation issues. 

### **CRAN** related issues

As in any process, they are flaws. Here are the ones I met using **CRAN** 
delivery information.

Information email is not always working correctly. From the analysis I can do, 
considering the 3 packages submission I did, many differences exists. Main 
issue is emailing, as I did not received the same emails for each of 
the packages and some emails are simply missing (either not sent, or not 
delivered). 

Compilation process of a package on many platforms brings also some weirdness. 
I received only confirmation for windows that is the platform I am the less 
interested in.  Got no information for other platforms (DEBIAN, OSX, UBUNTU, ...).
Finally, I discovered online that some of them were able to process correctly the 
package, while some others were not. Introspection of log files has shown that
issues where operating system context related and under **CRAN** responsibility (PDF 
compilations requires some extraneous packages on Solaris, bug on OSX). This has
been fixed by **CRAN** team.  

Last and probably the most disturbing was that I often faced some delays in the process because I did not received or did not know what was expected from me by the **CRAN** as improvements. Distinguishing a **CRAN** change request from a **CRAN** comment is not so easy, in received emails. Some issues (especially notes) arise but are not real issues. For example, your last name might not be recognize by the English dictionnary, thus generating a note. Identifying all the changes from a **CRAN** request is also not as easy as it should. I think that's rather a matter of presentation - due to email - than a matter of content itself. 


# A final word

CRAN team does a great and uneasy job. They often face same issues from R 
package submitters, and so they have to deal with very repetitive tasks. Nevertheless,
they keep things simple and oriented toward delivery. 

As a result of my return on experience, I have two improvement suggestions that could alleviate several pains.

Primo, I really believe that being able to run the same automated verifications as **CRAN**, will reduce the forth and back on a package submission. This will contribute to reduce **CRAN** burden for automated checks while leaving more time for human inspection. 

Secundo, for any submitted package, a submission process summary html page will be helpful  to share submission process status, progress and next steps, without any ambiguities. Having such a page as submission process summary will avoid loss of time and make clear the leader for the next action. This will also avoid deadlocks where each part awaits the other one, as each believe the other part is currently owning the lead. That will streamline and accelerate the whole process, especially in case of many re-submissions. 





