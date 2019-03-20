---
title: Scala Methods – Syntax, Declaration, Use case, Examples
tags: ["Scala", "Tutorial"]
date: 2019-01-02
excerpt: Scala methods and lambda. How to use them, write them, declare them with use cases, interactive code and practical examples.
---

Original Source: [scala-methods on Leobenkel.com](https://leobenkel.com/2019/01/scala-methods/).

## Introduction to Scala Methods

![Scala Logo](/assets/scala_logo.png)

In order to understand this article, one should understand [Scala Variables](https://leobenkel.com/2018/12/scala-variables/). After learning about Scala Variables, you can learn about Scala Methods.

## What is a method?

A method, sometimes called a function, in computer programming, is a black box which takes input(s), executes one or more operations, and finally yields an output value.

For instance, there might be a black box called `add` which would combine two values, `a` and `b`, and sum them together.

For the below example the values are 1 and 2.

```
1 and 2 -> add -> 3 (output)
```

In this case, the black box (add) contains `a + b`.

In computer science:

* the inputs are called arguments
* the black box is called a method or a function
* the output of the black box is called the return value

## How to declare a Scala Method ?

The keyword to declare a Scala method is `def`.

Below, find an example of a method to add two numbers.

```Scala
def add(a: Int, b: Int): Int = {
  a + b
}
```

Detailed review of the syntax:

* `def` declares the start of a method
* `add` is the name of the method
* In between `(` and `)`, find the arguments of the method, separated by coma , :
    * `a: Int` is the first argument
    * `b: Int` is the second argument
* After the arguments, `:` precedes the type of the return value of the method, in this example, we have `: Int`
* `=` declares the start of the content of the method
* `{` opens the context
* `a + b` is what the method will do with the arguments ( the content of the black box )
* `}` closes the context

*For those with proficiency in other computer languages:*
Other computer languages commonly use the keyword `return` to return the output of a method. In Scala, the last statement of a context is its return value.

## Bonus: What is a context in Scala ?

This section is aimed at those with proficiency in other computer languages. Feel free to jump to the next section, How to shorten method syntax, if you are a beginner.

A context is a block of code that has a return value. Values and variables declared within a context are destroyed when exiting the context. Scala is built on top of the [Java Virtual Machine (JVM)](https://www.wikiwand.com/en/Java_virtual_machine) so the garbage collector is going to remove unused variables.

In the example below, a context is being opened to set the value `name`. This context allows the execution of more code before determining the value of `name`. For instance, methods can be called.

```Scala
val name = {
  // do more things, like calling methods:
  val temporaryValue = generateRandomName()
  temporaryValue + "_123"
}
```

## How to shorten the syntax to declare a method ?

The context declaration can be omitted when there is only one line of code in the method:

```Scala
def add(a: Int, b: Int): Int = a + b
```

It is also possible to omit the return type of the method:

```Scala
def add(a: Int, b: Int) = a + b
```

But adding the return type will generally speed up the compilation process, [read more about it on this Reddit thread](https://www.reddit.com/r/scala/comments/9fiz75/if_i_define_a_return_type_for_every_method_would/).

## How to use a Scala Method ?

The example below shows how to use a declared method, following the syntax explained above.

```Scala
val output = add(1, 2)
```

Call the name of the method, `add`, and give it the values that `a` and `b` should be: `1` and `2`. In this example, `output` will take the value `3`.

## Practical example of Scala Methods

Below you can find a sandbox environment to practice declaring and using Scala Methods.

```Scala
def multiply(a: Double, b: Double): Double = {
  a * b
}

val weeksPerMonth = 4
val monthsPerYear = 12

val weeksPerYear = multiply(weeksPerMonth, monthsPerYear)

println(weeksPerYear)
```

Feel free to play with it.

If this does not work, [directly go to Scastie](https://scastie.scala-lang.org/IRy34COCSHGpbK4VGHMxlw).

## Bonus: Declare a method as a value

This section is aimed at those with proficiency in other computer languages. Feel free to jump to the next section, *What to remember*, if you are a beginner.

In Scala, you can declare `lambda` method. There is a [Stackoverflow post about Lambda method](https://stackoverflow.com/a/16509/3357831) you can read to learn more about the [theory behind it](https://en.wikipedia.org/wiki/Lambda_calculus).

Below find the first part of declaring a method as a value, starting by the type:

```Scala
val myMethod: InputType => OutputType
```

`val` declares an immutable variable, otherwise called a value.

Then, the `:` precedes the type.

Finally, there is the type `InputType => OutputType`, the `=>` operator are telling Scala that the Type of this value is going to transform `InputType` into `OutputType` when used.

See a working example below:

```Scala
val triple: Double => Double = _ * 3
```

`_` is a new piece of syntax: it is a wildcard to replace variables. `_` is used often within Scala code.

Here, it works in combination with the Type. Since the type is `Double` to `Double` ( `=>` can be read as “to” or “transforming into” ) , then `_` can only be of type `Double`.

To use this value `triple`, see the example below:

```Scala
val output = triple(5)
```

Use a method as a value in the same way as if it was a normal method.

## Practical example of Scala Lambda Method

Below you can find a sandbox environment to practice declaring and using Scala Lambda Methods.

```Scala
val triple: Double => Double = _ * 3

triple(4)
```

Feel free to play with it.

If this does not work, [go directly to Scastie](https://scastie.scala-lang.org/mRym8NZiRIStxprUR9xrmw).

## What to remember?

A few things to remember about Scala methods:

* `def` is to start the declaration of the method
* `(` and `)` encapsulate the argument(s) of the method
* `:` declares the return type of the method. Same as for Scala Variable
* `=` announces the start of the content of the method
* `{` and `}` encapsulate the context of the method
* `=>` declares a lambda method type
* `_` replaces a variable implicitly

## Conclusion

You now have the tools to use methods in Scala code.

Feel free to leave comments if you have any questions.

