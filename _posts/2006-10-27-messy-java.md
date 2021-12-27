---
layout: post
title: Messy Java code
category: category-linuxverse
summary: Java simplicity or so, as often said
image: images/linux/java.png
# comments: true
permalink: lv-mjc
---

### How easy is it to create Java messy code ?
It is often said that Java is simple. Simple to write,
simple to create a new program. Let's have a closer look to this statement and try to show that it only relies on conventions. 

### Foreseing a result in Java
The Java language has greatly simplified the coding. First, it is a strongly typed language. Second, some tricky classical features of languages have disapeared: no pointer as in <cite class="kw">C</cite> or <cite class="k<">C++</cite>, no precompilation phase, ... We could continue to enumerate a long list of features, all contributing to Java simplicity. It seems at the first glance, that the assertion is true. 

Of course, we could enter a great Java obfuscation contest, and come with a counter example that will prove that Java could be messy too! This is not what we would like to prove. We would like to show that using standard Java coding technics and practices, we could end up very easily to a difficult-to-predict result. Let's try to create a such short program. 
### Our two classes example
Let's consider the two following Java class definitions. The first class has two methods and a main. The second one holds two methods. All the class methods are composed by only one instruction. It cannot be simpler.<br/><br/> Could you figure out what will be the output of the program ?
#### first class
```java
package uc2;

public class _1 {
	private final int _;
	public _1 (int __) { _ = __;}
	public String __ () { return "" + _; }
	
	public static void main(String[] _) {
            _l_._l(new _1(_.length == 0 ? 1 : _l_.l_(_[0])).__());
	}
}
```

#### second class
```java
package uc2;

public class _l_ {
	public static void _l(String _) { System.out.println(_); }
	public static int  l_(String _) { return Integer.parseInt(_); }
}
```

#### Getting the result
For your information, the right result is displayed below. 

All we wanted to show, is that from a really simple Java example,

#### Run without argument
```java
1
```

####Run with the integer 1234 as argument
```java
1234
```

#### Run with the string "java is not so simple" as argument
```java
Exception in thread "main" java.lang.NumberFormatException: 
For input string: "java is not so simple"
  at java.lang.NumberFormatException.forInputString(...:48)
  at java.lang.Integer.parseInt(Integer.java:447)
  at java.lang.Integer.parseInt(Integer.java:497)
  at uc2._l_.l_(_l_.java:9)
  at uc2._1.main(_1.java:13)
java Result: 1
```
The result is the string representation of the first argument passed
to the program, considered to be an integer. If no parameter is given,
the result defaults to <cite class="code">1</cite>. If the first argument is not convertible to
an integer, then a <cite class="code">java.lang.NumberFormatException</cite> is
thrown. 

Did you discover the full solution ?


### So, is Java messy ?
From a really simple Java example, it appears counter intuitive and
difficult to guess the right result. Of course, an attentive and
constant reading could help. This example shows that the mental effort
to produce in order to understand the program behavior, and to guess
the right result is much harder than foreseen. 

It is a best practice to impose its own presentation and naming rules
to avoid such situations. Nevertheless, going to far this way, could
lead to an extraneous amount of work to conform to this naming rules.

Who knows about a rewritting application, that should help the reader to
understand better the written version, without having to produce a
great effort ? Imagine the strength of a such application, that will greatly
simplify the maintenance, an therefore, cut down its costs.

