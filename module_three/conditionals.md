# Conditional Statements/Expressions

## What Are Conditional Statements?

Conditional statements are statements which make a decision based on a condition. This condition could be a number 
of things, so it depends on what kind of conditional statement you're using.

## Types of Conditional Statements

### If-statements

#### Basic If-statements

If-statements are conditional statements which make a decision based on a boolean value. If the boolean value is 
`true`, the body of the if-statement is executed. If the boolean value is `false`, the body of the if-statement is 
skipped. The following code demonstrates the simplest kind of if-statements.

```java
if (true) { IO.println("Hello, world!"); }
if (false) { IO.println("Goodbye, world!"); }
```

The above code outputs the following to the console.

```text
Hello, world!
```

The syntax for an if-statement starts with the `if` keyword. It is followed by the boolean condition wrapped in 
parentheses. The body of the if-statement is then specified in curly brackets. If there is only one line's worth of 
code in an if-statement, it's common to see it written on one line. If there are multiple lines, they will appear 
after the `if` keyword and the condition as demonstrated by the following code.

```java
if (true) {
    IO.println("This will always run!");
    IO.println("Hello, world!");
}
```

One important thing to understand about if-statements in Java is that they only actually accept one statement to run 
as their bodies. This seems strange considering the previous if-statement had a two line body! It turns out the 
curly brackets are actually grouping the two statements into one by forming a code block. The if-statement then 
executes this code block. This means the curly brackets are optional for one-line if-statements as far as Java's 
syntax is concerned.

```java
if (true) IO.println("Hello, world!");
if (false)
    IO.println("Goodbye, world!");
```

Both of the above if-statements are valid in Java. However, there's a bit of a problem when we write if-statements 
without brackets. What do you think the output of the following code is?

```java
if (true)
    IO.println("Hello, world!");
    IO.println("Hello, again, world!");
```

If you guessed the following output, you'd be right!

```text
Hello, world!
Hello, again, world!
```

So what's the issue? Let's play this game again. What do you think the output of the following code is?

```java
if (false)
    IO.println("Goodbye, world!");
    IO.println("Just kidding!");
```

The above code outputs the following to the console.

```text
Just kidding!
```

Remember that if-statements only accept one statement as their body. This means only the next line is part of the 
body of an if-statement if the if-statement doesn't use brackets. Any lines after that, even if they're indented, 
won't be part of the body of the if-statement.

Now it might seem like the solution is to use brackets when there are multiple lines, but omit them when there's 
only one line! It would certainly be this simple if the omission of curly brackets didn't lead to bringing down the 
entire AT&T network on the East Coast! It seems so innocuous, but it can cause real problems. The reason is that 
someone may come along and wish to add code to an if-statement, but they may not realize there aren't any brackets 
if it was previously one line. This means they may write an if-statement like the one above where the indentation 
makes it seem like everything is okay, but it's not. This means you should ***always use brackets when writing 
if-statements***! It's only a few more characters to type, and it results in safer code!

Let's take a look at a non-trivial if-statements. We can use standard relational operators to do comparisons in 
if-statements.

```java
final var number = Integer.parseInt(IO.readln("Enter a number: "));
if (number > 0) { IO.println("You entered a positive number!"); }
```

`number > 0` returns a boolean, so the if-statement simply uses the result of the comparison to decide whether to 
run the code.

#### If-blocks

Each if-statement is what's known as an *if-block*. If-blocks are conditional blocks constructed from an if-statement; 
zero or more else-if-clauses; and zero or one else-clauses. Else-if-clauses allow for us to specify additional 
conditions to check if none of the preceding conditions were `true`. Else-clauses allow us to specify a catch-all 
statement which will run if none of the conditions in an if-block were `true`. The following code demonstrates using 
else-if-clauses and an else-clause to check multiple conditions.

```java
final var number = Integer.parseInt(IO.readln("Enter a number: "));
if (number < 0) {
    IO.println("You entered a negative number!");
} else if (number == 0) {
    IO.println("You entered zero!");
} else if (number < 10) {
    IO.println("You entered a single positive digit!");
} else {
    IO.println("You entered something else!");
}
```

It's important to note how this is different from simply using four if-statements in a row. In an if-block, 
conditions are only checked until a `true` condition is found. If a `true` condition is found, the body of the 
associated statement runs, then the if-block is done. No remaining conditions will be checked. With four 
if-statements in a row, each condition will be checked regardless of the outcome of the previous conditions. Whether 
you want a bunch of if-statements or one if-block simply depends on what type of logic you need. Take a look at the 
output of the previous code.

```text
Enter a number: -1
You entered a negative number!
```

Notice how only the if-statement ran? `number < 0` was `true`, so the if-statement ran, then since the other 
statements were part of the same if-block, they were skipped. Let's take a look at the same code, but using four 
if-statements instead of one if-block.

```java
final var number = Integer.parseInt(IO.readln("Enter a number: "));
if (number < 0) {
    IO.println("You entered a negative number!");
}
if (number == 0) {
    IO.println("You entered zero!");
}
if (number < 10) {
    IO.println("You entered a single positive digit!");
}
if (number >= 10) {
    IO.println("You entered something else!");
}
```

Let's see how the output differs for the same input.

```text
Enter a number: -1
You entered a negative number!
You entered a single positive digit!
```

Notice how some extra text printed that doesn't make sense? That's because the previous code was relying on if-block 
logic to prevent later statements from running if a preceding statement was `true`. To make the new code act like the 
old code, we would need to change the third condition `number < 10` to `number > 0 && number < 10`.

### Switch-statements

Switch-statements are another kind of conditional statement in C#. Switch-statements work by taking in a value and 
checking different cases for that value to decide what to do. Switch-statements are useful when we want to do 
different things based on a particular value.

#### Basic Switch-statements

The following example shows how to use a switch statement to print 
different things depending on the value of a number.

```java
final var number = Integer.parseInt(IO.readln("Enter a number: "));
switch (number) {
    case 0       -> IO.println("You entered zero!");
    case 1, 2, 3 -> IO.println("You entered one, two, or three!");
    default      -> IO.println("You entered something else!");
}
```

Each case has a particular value or set of values to compare with the value in `number`. These values are called 
*labels*. If the value in `number` is equivalent to the label or labels for a particular case, the code for that case 
will be run. The default case runs if none of the preceding cases match.

The default case is optional. If the default case is included, it must be the last case since Java doesn't allow 
earlier switch-cases to dominate later switch-cases.

Switch cases are matched in the order they're written in most situations.

The above code outputs the following for different cases.

```text
Enter a number: 0
You entered zero!
```

```text
Enter a number: 1
You entered one, two, or three!
```

```text
Enter a number: 2
You entered one, two, or three!
```

```text
Enter a number: -1
You entered something else!
```

One thing to note is that it's not necessary to align the arrows of each switch-case. This is a stylistic choice, so 
you can either follow it or ignore it! Java won't care either way.

It's possible to include multiple lines of code in a switch-case by using curly brackets after the arrow. Unlike with 
if-statements, a syntax error will be raised if we attempt to write multiple lines of code for a switch-case without 
writing curly brackets, so it's okay to omit them when only one line of code is written.

```java
final var number = Integer.parseInt(IO.readln("Enter a number: "));
switch (number) {
    case 0    -> IO.println("You entered a zero, so I won't to anything");
    case 1, 2 -> {
        final var sum = number + 5;
        IO.println("Your number plus five is %d".formatted(sum));
    }
    default   -> IO.println("You entered something else");
}
```

The above code outputs the following in different cases.

```text
Enter a number: 0
You entered zero, so I won't do anything
```

```text
Enter a number: 1
Your number plus five is 6
```

```text
Enter a number: 3
You entered something else
```

#### Switch-statements with Guarded Pattern Labels

The previous switch-statement examples all used *constant labels* as their case labels. Constant labels are labels 
which represent literals. This is useful for certain situations, but sometimes we want to qualify a label. Is it 
possible to write a case that matches a value only if that value is within a certain range? Yes, with a *guarded 
pattern label*! Guarded pattern labels are labels which let us specify a requirement for a match. To write a guarded 
pattern label, we first have to write a pattern label, which looks like a simple variable declaration. We then write a 
when-clause with a guard which is a boolean expression. The case will only match if the value passes the guard. The 
following example shows how to write guarded pattern labels.

```java
final var number = Integer.parseInt(IO.readln("Enter a number: "));
switch (number) {
    case 0                 -> IO.println("You entered zero!");
    case int i when i < 0  -> IO.println("You entered a negative number!");
    case int i when i < 10 -> IO.println("You entered a single positive digit!");
    default                -> IO.println("You entered something else!");
}
```

The above code does the same thing as the if-block in a previous example. Java first checks the constant label `0`. If 
that label doesn't match, Java then checks the first guarded pattern label where it assigns the value in `number` to 
the newly declared pattern variable `i`, then checks the guard. If that label doesn't match, Java then checks the next 
guarded pattern label in the same way. Since switch-cases are checked in order, we don't have to worry about negative 
numbers matching the second guarded pattern label!

When constant labels and guarded pattern labels are used in the same switch statement, the convention is to write 
constant labels first followed by guarded pattern labels. This helps avoid issues with guarded pattern labels 
dominating constant labels.

Let's now look at checking multiple guards in a switch-case.

```java
final var number = Integer.parseInt(IO.readln("Enter a number: "));
switch (number) {
    case int i when i > 0 && i < 9   -> IO.println("Single digit");
    case int i when i < 0 || i > 100 -> IO.println("Negative number or number greater than 100");
    default                          -> IO.println("Something else");
}
```

Since guards are boolean expressions, we can include multiple guards by using logical operators.

Switch-statements can be used with values of any type. The following code demonstrates switching on a string.

```java
final String word = IO.readln("Enter a word: ");
switch (word.toLowerCase()) {
    case "hello" -> IO.println("Hey, there!");
    case "goodbye" -> IO.println("You're already leaving?");
    default -> IO.println("That's a nice word!");
}
```

This can be an alternative to writing an if-block doing a bunch of case-insensitive equality comparisons.

## What Are Conditional Expressions?

Conditional expressions are expressions which evaluate to a value based on the result of a condition. Conditional 
expressions can be a compact way to decide between several values.

## Types of Conditional Expressions

### Ternary Expression

Ternary expressions are expressions formed using the *ternary operator* (`?:`). The ternary operator is an 
interesting operator because it's the only operator that accepts three arguments. This is actually where it gets its 
name: *unary* operators accept one argument, *binary* operators accept two arguments, and *ternary* operators accept 
three arguments. Since it's the only operator that accepts three arguments, it became known as the ternary operator.

Ternary expressions are used to decide between one of two values depending on the value of a boolean expression. The 
following code demonstrates using a ternary expression to display the result of an evenness check in a user-friendly 
way.

```java
final var number = Integer.parseInt(IO.readln("Enter an integer: "));
final var result = number % 2 == 0 ? "even" : "odd";
IO.println("Your number is %s".formatted(result));
```

The above code outputs the following to the console.

```text
Enter an integer: 3
Your number is odd
```

Ternary expressions are written as `condition ? valueIfTrue : valueIfFalse`. In the above example, the number 3 is 
odd, so `number % 2 == 0` returned `false`, meaning the ternary expression evaluated to `"odd"`.

We could have written the above code a bit more compactly by writing the ternary expression inside the parentheses for 
the `formatted` method call. The following code demonstrates this.

```java
final var number = Integer.parseInt(IO.readln("Enter an integer: "));
IO.println("Your number is %s".formatted(number % 2 == 0 ? "even" : "odd"));
```

### Switch Expressions

Switch statements have an expression version. Switch expressions follow the same logic as switch statements but they're 
written a little differently in some cases. They are also evaluated since they are expressions. The following code 
demonstrates using a switch expression to print one of three possible messages depending on the number a user enters.

```java
final var number = Integer.parseInt(IO.readln("Enter an integer: "));
IO.println(switch (number) {
    case 0                -> "Zero is an interesting number";
    case int i when i < 0 -> "Negative numbers are pretty cool";
    default               -> "Positive numbers are a little less cool, but still pretty cool";
});
```

The above code outputs the following to the console.

```text
Enter an integer: -4
Negative numbers are pretty cool
```

In switch expressions, the values or objects that come after each `->` are what the switch expression will evaluate to 
if the corresponding case is matched.

One important thing to note is that switch expressions must be *exhaustive*. This means switch expressions will 
raise a syntax error if none of the provided cases match an object or value. In the above example, any integer could 
attempt to be matched, and no matter what the integer is, it will always match one case.

We're able to include branches with multiple lines of code, but this requires the use of the `yield` keyword to signal 
the value of a particular branch. The following example demonstrates a branch with multiple lines of code.

```java
final var number = Integer.parseInt(IO.readln("Enter an integer: "));
IO.println(switch (number) {
    case 0                -> "Zero is an interesting number";
    case int i when i < 0 -> {
        final int result = i + 5;
        yield "Your number plus five is %d".formatted(result);
    }
    default               -> "Positive numbers are a little less cool, but still pretty cool";
});
```

The above code outputs the following in different cases.

```text
Enter an integer: 0
Zero is an interesting number
```

```text
Enter an integer: -4
Your number plus five is 1
```

```text
Enter an integer: 4
Positive numbers are a little less cool, but still pretty cool
```
