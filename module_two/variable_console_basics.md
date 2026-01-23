# Variable and Console Basics

## Exploring a Hello-world Project

```java
void main() {
    IO.println("Hello, world!");
}
```

Let's break this down into two pieces.

### `main` Method

```java
void main() {
    
}
```

This is the `main` method. Methods are a type of function, but we won't worry about that distinction just yet. For 
now, think of functions and methods as being the same thing.

This method serves as the entrypoint for a Java application. All Java applications are required to have at least one 
`main` method. When you run a Java application, your code will start executing from the first line of the `main` method.

```java
IO.println("Hello, world!");
```

This is a Java print statement. It prints the text "Hello, world!" to the console followed by a newline. This is the
print statement you'll use most of the time.

Java requires semicolons at the end of all statements. This tells the compiler when a thought is complete.

## Comments

```java
// Single-line comment.
/*
Multiline
comment.
*/
```

The above code shows how to write single-line and multi-line comments. Multiline comments are only used in a few select
situations, so you should stick to single-line comments. Single-line comments last from `//` to the end of the line.
Multi-line comments last from `/*` to `*/`.

## Basic Data Types

The following table shows the basic Java data types and some information about them.

| Type      | Wrapper Type | Size in Bits | Zero Value | Classification                      |
|-----------|--------------|--------------|------------|-------------------------------------|
| `boolean` | `Boolean`    | 8            | `false`    | Integral                            |
| `byte`    | `Byte`       | 8            | `0`        | Integral                            |
| `char`    | `Character`  | 16           | `'\0'`     | Unicode (UTF-16)                    |
| `short`   | `Short`      | 16           | `0`        | Integral                            |
| `int`     | `Integer`    | 32           | `0`        | Integral                            |
| `float`   | `Float`      | 32           | `0.0F`     | Binary Floating-point (binary32)    |
| `long`    | `Long`       | 64           | `0L`       | Integral                            |
| `double`  | `Double`     | 64           | `0.0`      | Binary Floating-point (binary64)    |
| `String`  | N/A          | Unspecified  | `""`       | Unicode Sequence (UTF-16)           |

Each of the above types has a wrapper type. This wrapper type is where a bunch of useful methods for working with 
these types come from. We'll learn what we can use the wrapper types for in a later section.

Let's go over the type classifications

### Integral

Integral types are used for storing integers.

### Floating-point

Floating-point types are used for representing rational and irrational numbers (approximated). Java follows the
IEEE-754 standard for floating-point numbers, which is what most languages follow. In this course, we won't worry about
how floating-point numbers are stored, but you are welcome to investigate this if you want to!

#### Binary Floating-point

Binary floating-point types store values in binary. These types are subject to errors due to the conversion from
decimal to binary. These types should not be used when accuracy is critical. We'll learn what to do when accuracy 
matters later on.

### Unicode

Unicode is how computers encode characters. Unicode replaced ASCII when computers started needing to be able to
represent more than 128 unique characters. There are three versions of Unicode: UTF-8, UTF-16, and UTF-32. We won't
be getting into Unicode in this course, but it's worth noting that Java uses UTF-16, which means characters are
represented using either 16 bits or 32 bits.

### Primitive vs. Non-primitive Types

Except for `String`, the above types are all considered *primitive types*. Primitive types represent numbers. These
are the foundational building blocks of other types. The other types are considered *non-primitive types* since
they are built out of primitive types. `String` is an example of a non-primitive type since it's a sequence of `char`s.

Primitive and non-primitive are represented differently in Java, and we'll learn the specifics of this in a later 
module. For now, the most important difference to understand is that primitive values don't have methods, whereas 
non-primitive objects do. This means primitive values can't do anything other than exist, whereas non-primitive 
objects can perform abilities. We'll see some examples with the `String` type in this lesson.

## Variables

The syntax for variables in Java is as follows.

```java
<type> <name> = <value>;
```

Let's say we want to declare an `int` variable. The following code shows how to do this.

```java
int number = 5;
```

### Naming Conventions

Java uses camelCase for naming local variables. Java also prefers using full words over abbreviations. That's why the
above variable was named `number` instead of `num`. When it comes to acronyms and initialisms, they should only be
used when widely recognized. They should also act like words when it comes to capitalization. The following code
demonstrates proper capitalization of acronyms and initialisms in Java.

```c#
int idNumber = 1; // all lowercase at beginning
int studentId = 2; // first letter capitalized when in middle or at end
```

### Global Variables

Java allows us to declare variables outside of methods. While these variables aren't technically global variables 
given the way Java works, we can think of them like global variables since they work almost identically. Global 
variables are created the same way as regular variables, except they're declared outside of methods. Global 
variables should always be declared at the top of your code.

```java
int globalNumber = 7;

void main() {
    // Main code.
}
```

### `var` keyword

The `var` keyword can be used in place of a type to have Java deduce the type from the right-hand side. You should use
the `var` keyword whenever the type is obvious, or when the readability of your code can be enhanced. This means the
following is preferred.

```java
var number = 5;
```

This keyword will also allow us to avoid repeating data types later on when we start using other data types.

The `var` keyword can only be used when declaring local variables. When declaring global variables, concrete types 
must be used.

```java
// var globalNumber = 5; // won't compile
int globalNumber = 5; // works

void main() {
    var localNumber = 5; // works;
//    int localNumber = 5; // works, but `var` is preferred since type is obvious
}
```

### Final Variables

Final variables are variables that can't be reassigned to other values. In other words, the first value assigned to 
a final variable is the final value that variable will ever have. The following code demonstrates creating a final 
variable.

```java
final var g = 9.81;
```

Variables should be declared final whenever possible. This allows Java to potentially perform optimizations to make 
our code faster. It also makes it easier to see which variables will be changing in our code and which variables 
will remain a constant value.

When declaring a final global variable, we would consider this to be a *global constant*. When naming global 
constants in Java, we use SCREAMING_SNAKE_CASE instead of camelCase to denote this.

```java
final int GLOBAL_CONSTANT = 14;

void main() {
    // Main code.
}
```

## Console Output

The following code demonstrates the two methods we can use to output text to the console.

```java
IO.println("Hello, world!");
IO.print("Hello, ");
IO.println("world!");
```

The above code produces the following output.

```text
Hello, world!
Hello, world!
```

The `IO.println` method outputs text followed by a newline character. The `IO.print` method outputs text
with no trailing newline.

## Formatted Strings

It's very common to want to insert values into strings. Java supports string concatenation, so we could output the
value of a variable as shown in the following code.

```java
final var luckyNumber = 7;
IO.println("I think " + luckyNumber + " is my lucky number!");
```

While this works, it can be hard to keep track of where to put spaces to make sure the output looks right. It can
also become fairly unreadable when a lot of concatenation is used. To solve this problem, Java offers *formatted
strings* which are strings that outline a template where values can be inserted later. The following code shows how to 
use a formatted string to do the same thing as the above code.

```java
final var luckyNumber = 7;
IO.println("I think %d is my lucky number!".formatted(luckyNumber));
```

The `%d` symbol is known as a *verb*, and it acts as a placeholder for an integer value. That value is then supplied 
by calling the `formatted` method. Formatted strings are a bit clunky because they require different verbs depending 
on the types of the values you'll be substituting. Java may support a better way for substituting values into strings 
in the future, but for now, this is what we get.

The following sections show the different verbs and their corresponding types. They also showcase a few different 
types of verbs which substitute values in different ways for given types.

### Integral Verbs

* `boolean`

| Verb | Function                                 |
|------|------------------------------------------|
| `%b` | Substitutes a boolean value in lowercase |
| `%B` | Substitutes a boolean value in uppercase |

* `char`

| Verb | Function                                   |
|------|--------------------------------------------|
| `%c` | Substitutes a character value in lowercase |
| `%C` | Substitutes a character value in uppercase |

* `byte`, `short`, `int`, `long`

| Verb | Function                                                           |
|------|--------------------------------------------------------------------|
| `%o` | Substitutes an integer value in octal                              |
| `%d` | Substitutes an integer value in decimal                            |
| `%x` | Substitutes an integer value in hexadecimal with lowercase letters |
| `%X` | Substitutes an integer value in hexadecimal with uppercase letters |

### Floating-point Verbs

* `float`, `double`

| Verb | Function                                                                        |
|------|---------------------------------------------------------------------------------|
| `%f` | Substitutes a floating-point value in standard notation                         |
| `%e` | Substitutes a floating-point value in scientific notation with a lowercase 'e'  |
| `%E` | Substitutes a floating-point value in scientific notation with an uppercase 'E' |
| `%g` | Substitutes the shortest representation between `%f` and `%e`                   |
| `%G` | Substitutes the shortest representation between `%f` and `%E`                   |

### `String` verbs

| Verb | Function                                 |
|------|------------------------------------------|
| `%s` | Substitutes a string object in lowercase |
| `%S` | Substitutes a string object in uppercase |

This is not an exhaustive list, but it's the verbs you'll want to use most often. We'll learn about a couple other 
verbs when we need them in later modules. Let's take a look at substituting multiple values using a formatted string.

```java
IO.println("My name is %s, and I like the number %d".formatted("John", 15));
```

The above code outputs the following to the console.

```text
My name is John, and I like the number 15
```

The values are substituted in order when there is more than one. There are other things we can do with formatted 
strings which we'll learn about in later modules. Formatted strings should be preferred over string concatenation 
unless what's being concatenated is super simple.

## Console Input

### Getting String Input

We use the `IO.readln` method to get input in Java. The following code demonstrates how to use this method.

```java
final String name = IO.readln("Enter your name: ");
IO.println("It's nice to meet you, %s".formatted(name));
```

The `IO.readln` method will pause the program until the user types something into the console and presses the
RETURN key. The code will the proceed as normal.

### Getting Input of Other Types

`IO.readln` always returns `String`, so what do we do if we want to accept an integer? We use those Java wrapper types
we learned about earlier to convert string input to other types. The following code shows how to accept integer input.

```java
final var age = Byte.parseByte(IO.readln("Enter your age: "));
IO.println("You're %d year(s) old".formatted(age));
```

There are conversion methods for converting from a string to every other basic type. Simply use the wrapper type 
and corresponding method for whichever primitive type you want. Something else to know is that each conversion method 
will throw an exception if it's not possible to convert the string to the requested type. This is a problem if we 
want our code to handle bad input. We'll learn how to deal with this in a later module, so for now, assume the user 
always enters input perfectly.

You now know enough to create a basic chatbot!
