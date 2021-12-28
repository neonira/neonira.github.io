---
layout: post
title: Artificial intelligence glossary
category: category-linuxverse
summary: Java simplicity or so, as often said
image: images/linux/ia.jpg
# comments: true
permalink: lv-ia-1
---

### Preamble
All the terms are given and to be understood in the scope of <cite class='kw'>AI</cite>. Many of them, have several meanings. Do not get trapped by the meaning. Know what you aim to. 

### Underlying mathematical concepts

1. <a name="gradient"></a>**gradient**  
Vector containing the function variation, in regards to its different parameters
<cite class='ref'>[wikipedia en](https://en.wikipedia.org/wiki/Gradient), [wikipedia fr](https://fr.wikipedia.org/wiki/Gradient)</cite>

1. **Jacobian**  
Matrix holding the partial derivatives of a function  
<cite class='ref'>[wikipedia en](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant), [wikipedia fr](https://fr.wikipedia.org/wiki/Matrice_jacobienne)</cite>

1. **Hessian**  
Matrix holding second order partial derivatives of a function  
<cite class='ref'>[wikipedia en](https://en.wikipedia.org/wiki/Hessian_matrix), [wikipedia fr](https://fr.wikipedia.org/wiki/Matrice_hessienne)</cite>

1. **nabla**  
Alias of [gradient](#gradient)

### Software engineering concepts
1. <a name='recycling'></a>**recycling, broadcasting**  
Each of these terms refers to the special ability to proceed to N-dimension matrix operations without strict compliance to mathematics requirements. 
For example, adding two matrices requires that they share exactly the same dimensions. Under software engineering, these features allows you to get rid of such conditions, and the release the strict conditions to enter a loose conditioning. This is done by converting the N-dimensions matrix to a vector and resizing it to the target length. Many checks are done and generally when lengths do not match, an error/warning is emitted by the software library in charge of the calculus. This is a very convenient way to handle mathematical operations on N-dimensions.  
**recycling** it the official term used in <cite class='kw'>R language</cite>, while **broadcasting** is the official term used in <cite class='kw'>Python language</cite>. 

1. **vectorization**  
It is the programming language ability to proceed to a N-dimensions operation(s) while coding it as a simple mathematical operation. To sum three integers, x, y, and z, you'll write <code> result <- x + y + z </code>.  If your programming language owns this capability, then, x, y, and z, could be scalars, vectors, matrix, or N-dimension arrays. The code shown above will provide the right result, whatever the inputs.  Moreover, it will do so, considering [recycling, broadcasting](#recycling). Generally, vectorization ability is tied to operator overloading ability of the programming language.

### Artificial Intelligence concepts

1. **AI algorithmic general pattern**  
AI software generally follows the following simple pattern  
    1. compute forward propagation using the neural network model  
    1. compute loss  
    1. compute backward propagation  
    1. update the model parameters  

1. **forward propagation**  
tbd.

1. <a name="backpropagation"></a>**back propagation**  
Method to compute a gradient
<cite class='ref'>[wikipedia en](https://en.wikipedia.org/wiki/Backpropagation), [wikipedia fr](https://fr.wikipedia.org/wiki/R%C3%A9tropropagation_du_gradient)</cite>

1. **loss function**  
To compute loss, you will have to code a loss function, according to the model you are evaluating. Machine learning is the process that tends to reduce the loss in order to minimize ```𝓛(ŷ, y)```

1. **derivative computation methods**  
[Back propagation](#back propagation) phase in AI, is intimately tied to computation of derivatives in order to updates the model parameters. Several methods exists to do so, each of them bears advantages and limits. Here, you'll find a quick summary of the most common derivative computation methods.  

    1. **Mathematical derivative computation method**  
Given a mathematical function expression, you will use mathematical derivation techniques to compute the expression of the derivative, that you will code directly. This method requires to know the initial function expression and to be able to compute its derivative. Sometimes very complex to do so, but it always provides an exact result. 

    1. **Numerical differentiation computation method**  
This method approximates the derivative by computing the difference ```(f'(x + h) - f'(x)) / h```. The result is an approximation.

    1. **Symbolic differentiation computation method**  
This method relies on expression manipulation. It allows expressions to be transformed, according to symbol calculus, change of variable, and mathematical rules. It provides and exact result. It is generally done using a specialized mathematical tool as Mathlab for example. 

    1. **Algorithmic differentiation computation method**  
This method uses an algorithm to evaluation the derivative. It computes during the forward propagation both the value and its derivative, and it appears that the algorithm is not only providing exact results, it is also computationnaly efficient.  
This method is sometimes named **auto differentiation** or **autodiff**.  
<cite class='ref'>[autodiff v4](/documents/ai/autodiff.pdf)


