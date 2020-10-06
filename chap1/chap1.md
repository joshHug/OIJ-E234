# 1.1 Essentials

Let's look at our first Java program. When run, the program below prints "Hello world!" to the screen.

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

For those of you coming from a language like Python, this probably seems needlessly verbose. However, it's all for good reason, which we'll come to understand over the next couple of weeks. Some key syntactic features to notice:

* The program consists of a class declaration, which is declared using the keywords `public class`. In Java, all code lives inside of classes.
* The code that is run is inside of a method called `main`, which is declared as `public static void main(String[] args)`.
* We use curly braces `{` and `}` to denote the beginning and the end of a section of code.
* Statements must end with semi-colons.

This is not a Java textbook, so we won't be going over Java syntax in detail. If you'd like a reference, consider either Paul Hilfinger's free eBook [A Java Reference](http://www-inst.eecs.berkeley.edu/~cs61b/fa14/book1/java.pdf), or if you'd like a more traditional book, consider Kathy Sierra's and Bert Bates's [Head First Java](http://www.headfirstlabs.com/books/hfjava/).

For fun, see [Hello world! in other languages](https://www.rosettacode.org/wiki/Hello_world/Text).

## Variables and Loops

The program below will print out the integers from 0 through 9.

```java
public class HelloNumbers {
    public static void main(String[] args) {
        int x = 0;
        while (x < 10) {
            System.out.print(x + " ");
            x = x + 1;
        }
    }
}
```

When we run this program, we see:

```text
$ javac HelloNumbers.java
$ java HelloNumbers
$ 0 1 2 3 4 5 6 7 8 9 
```

Some interesting features of this program that might jump out at you:

* Our variable x must be declared before it is used, _and it must be given a type!_
* Our loop definition is contained inside of curly braces, and the boolean expression that is tested is contained inside of parentheses.
* Our print statement is just `System.out.print` instead of `System.out.println`. This means we should not include a newline \(a return\).
* Our print statement adds a number to a space. This makes sure the numbers don't run into each other. Try removing the space to see what happens. 
* When we run it, our prompt ends up on the same line as the numbers \(which you can fix in the following exercise if you'd like\).

Of these features the most important one is the fact that variables have a declared type. 

## Static Typing

One of the most important features of Java is that all variables and expressions have a so-called `static type`. Java variables can contain values of that type, and only that type. Furthermore, the type of a variable can never change.

One of the key features of the Java compiler is that it performs a static type check before the code is even allowed to run. For example, suppose we have the program below:

```java
public class HelloNumbers {
    public static void main(String[] args) {
        int x = 0;
        while (x < 10) {
            System.out.print(x + " ");
            x = x + 1;
        }
        x = "horse";
    }
}
```

If we try to compile this program, we'd get an error that  "String cannot be converted to int".

The compiler rejects this program out of hand before it even runs. This is a big deal, because it means that there's no chance that somebody running this program out in the world will ever run into a type error!

This is in contrast to dynamically typed languages like Python, where users can run into type errors during execution!

In addition to providing additional error checking, static types also let the programmer know exactly what sort of object he or she is working with. We'll see just how important this is in the coming weeks. This is one of my personal favorite Java features.

To summarize, static typing has the following advantages:

* The compiler ensures that all types are compatible, making it easier for the programmer to debug their code.
* Since the code is guaranteed to be free of type errors, users of your compiled programs will never run into type errors. For example, Android apps are written in Java, and are typically distributed only as .class files, i.e. in a compiled format. As a result, such applications should never crash due to a type error since they have already been checked by the compiler.
* Every variable, parameter, and function has a declared type, making it easier for a programmer to understand and reason about code.

However, we'll see that static typing comes with disadvantages, to be discussed in a later chapter.

## Defining Functions in Java

In languages like Python, functions can be declared anywhere, even outside of functions. For example, the code below declares a function that returns the larger of two arguments, and then uses this function to compute and print the larger of the numbers 8 and 10:

```python
def larger(x, y):
    if x > y:
        return x
    return y

print(larger(8, 10))
```

Since all Java code is part of a class, we must define functions so that they belong to some class. Functions that are part of a class are commonly called "methods". We will use the terms interchangably throughout the course. The equivalent Java program to the code above is as follows:

```java
public class LargerDemo {
    public static int larger(int x, int y) {
        if (x > y) {
            return x;
        }
        return y;
    }

    public static void main(String[] args) {
        System.out.println(larger(8, 10));
    }
}
```

The new piece of syntax here is that we declared our method using the keywords `public static`, which is a very rough analog of Python's `def` keyword. We will see alternate ways to declare methods in the next chapter.

The Java code given here certainly seems much more verbose! You might think that this sort of programming language will slow you down, and indeed it will, in the short term. Think of all of this stuff as safety equipment that we don't yet understand. When we're building small programs, it all seems superfluous. However, when we get to building large programs, we'll grow to appreciate all of the added complexity.

As an analogy, programming in Python can be a bit like [Dan Osman free-soloing Lover's Leap](https://www.youtube.com/watch?v=NCByLWtM7y4). It can be very fast, but dangerous. Java, by contrast is more like using ropes, helmets, etc. as in [this video](https://www.youtube.com/watch?v=tr6UIfPEuI0).

## Code Style, Comments, Javadoc

Code can be beautiful in many ways. It can be concise. It can be clever. It can be efficient. One of the least appreciated aspects of code by novices is code style. When you program as a novice, you are often single mindedly intent on getting it to work, without regard to ever looking at it again or having to maintain it over a long period of time.

In this course, we'll work hard to try to keep our code readable. Some of the most important features of good coding style are:

* Consistent style \(spacing, variable naming, brace style, etc\)
* Size \(lines that are not too wide, source files that are not too long\)
* Descriptive naming \(variables, functions, classes\), e.g. variables or functions with names like `year` or `getUserName` instead of `x` or `f`.
* Avoidance of repetitive code: You should almost never have two significant blocks of code that are nearly identical except for a few changes.
* Comments where appropriate. Line comments in Java use the `//` delimiter. Block \(a.k.a. multi-line comments\) comments use  `/*` and `*/`.

The golden rule is this: Write your code so that it is easy for a stranger to understand.

Often, we are willing to incur slight performance penalties, just so that our code is simpler to [grok](https://en.wikipedia.org/wiki/Grok). We will highlight examples in later chapters.

### Comments

We encourage you to write code that is self-documenting, i.e. by picking variable names and function names that make it easy to know exactly what's going on. However, this is not always enough. For example, if you are implementing a complex algorithm, you may need to add comments to describe your code. Your use of comments should be judicious. Through experience and exposure to others' code, you will get a feeling for when comments are most appropriate.

One special note is that all of your methods and almost all of your classes should be described in a comment using the so-called [Javadoc](https://en.wikipedia.org/wiki/Javadoc) format. In a Javadoc comment, the block comment starts with an extra asterisk, e.g. `/**`, and the comment often \(but not always\) contains descriptive tags. We won't discuss these tags in this textbook, but see the link above for a description of how they work.

As an example without tags:

```java
public class LargerDemo {
    /** Returns the larger of x and y. */           
    public static int larger(int x, int y) {
        if (x > y) {
            return x;
        }
        return y;
    }

    public static void main(String[] args) {
        System.out.println(larger(8, 10));
    }
}
```

The widely used [javadoc tool](http://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html) can be used to generate HTML descriptions of your code. We'll see examples in a later chapter.
