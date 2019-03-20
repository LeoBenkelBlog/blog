---
title: Scala Variables - Syntax, Declaration, Use case, Examples
tags: ["Scala", "Tutorial"]
date: 2018-12-12
---

Original Source: [scala-variables on Leobenkel.com](https://leobenkel.com/2018/12/scala-variables/).

## Introduction to Scala Variables

![Scala Logo](/assets/scala_logo.png)

After you have created your own Scala project, you can begin to write code. In this short article, we are going to learn how to use and set Scala variables.

## How to set Scala Variables?

If you want to declare a variable, you must use the keyword `var`.

```Scala
var variableName = 12
```

This line will declare a variable named `variableName` of value `12`.

## How to set Scala Values?

In Scala, we prefer to use `immutable` variables. You can [read why on StackOverflow](https://stackoverflow.com/a/6489497/3357831).

This is how you declare a value:

```Scala
val valueName = 12
```

This line will declare a value named `valueName` of value 12.

## How to declare the Type?

Variables will have a type inferred by the compiler. If you would like to add a type to your variable, you must use the `:` syntax.

```Scala
val name: String = "Leo Benkel"
```

In Scala, everything can be assigned to a value:

* integers, strings, …
* lambda functions
* class

We are going to talk more about the above in upcoming articles.

## What is the keyword `lazy` for?

You might have seen the keyword `lazy`.

```Scala
lazy val complexMath: Double = 10 * 10 * 10
```

In this instance, I am going to use `complexMath` as an example of a value. We could imagine this value as being long and costly to calculate.

With the keyword `lazy`, `complexMath`‘s value will only be computed once when used for the very first time.

The code used to generate `complexMath`‘s value will not be executed until it used for the first time.

Also, the value generated, in this case `complexMath`, will be stored and the code used to generate this value will not be executed again a second time.

## Practical example

Let’s go through a short example to practice what we have learned.

```Scala
val value: Int = 12
var variable: Int = 67

variable += 10

println(value)
println(variable)
```

Feel free to play with it.

If the playground above does not load, you can [go directly to Scastie](https://scastie.scala-lang.org/Dedjz4JwRzqhV0Z36BZbcw).

## What to remember?

A few things to remember about Scala variables:

to remember about Scala variables:

* `var` for mutable
* `val` for immutable
* Use immutable as much as possible and avoid using mutable
* Syntax is `val <name>:<type> = <value>`
* `lazy` will delay the evaluation of the value to the first use

## Conclusion

By understanding these basics, you should now be able to declare and use variables in Scala code.

Feel free to leave comments if you have any questions.










