# Boolean Expressions

*Boolean expressions* are expressions that return booleans. Boolean expressions can be as simple as a single boolean 
variable, or they can involve *equality operators*, *relational operators*, or *logical operators*.

## Equality Operators

Equality operators are operators that compare objects for equality. We will discuss comparing objects for equality 
in more detail later since there's more than initially meets the eye, but for now, we'll focus on simple value 
equality which is very straightforward. The following table shows the equality operators in Java.

| Name                | Operator |
|---------------------|----------|
| Equality Operator   | `==`     |
| Inequality Operator | `!=`     |

The above operators all return booleans to reflect the result of the comparison. The following code demonstrates
using the equality operator.

```java
IO.println("3 == 4: %b".formatted(3 == 4));
```

The above code outputs the following to the console.

```text
3 == 4: false
```

## Relational Operators

Relational operators are operators used for comparing objects. The following table shows the relational operators in 
Java.

| Name                           | Operator     |
|--------------------------------|--------------|
| Less-than Operator             | `<`          |
| Less-than-or-equal Operator    | `<=`         |
| Greater-than Operator          | `>`          |
| Greater-than-or-equal Operator | `>=`         |
| Instance-of Operator           | `instanceof` |

The above operators all return booleans to reflect the result of the comparison. The following code demonstrates 
using the less-than operator.

```java
IO.println("3 < 4: %b".formatted(3 < 4));
```

The above code outputs the following to the console.

```text
3 < 4: true
```

The other similar relational operators work the same way. The `instanceof` operator, however, works differently. We'll 
discuss this operator on its own later in the course, so you don't need to worry about it for now!

## Logical Operators

Logical operators are operators for combining or manipulating booleans. Each of these operators represents a 
fundamental operation for any computer. We will look at each operator one by one along with its *truth table* to 
understand how they work. When reading truth tables, *A* and *B* are arguments to the operator.

### Logical-and Operator

The logical-and operator (`&&`) evaluates to `true` if both arguments are `true`. Below is the truth table for the 
logical-and operator. *AB* is read as *A and B*.

| A | B | AB |
|---|---|----|
| F | F | F  |
| F | T | F  |
| T | F | F  |
| T | T | T  |

We can see that *A* and *B* must both be `true` for the logical-and operator to evaluate to `true`. The following code 
demonstrates using the logical-and operator.

```java
IO.println("3 is between 1 and 5: %b".formatted(1 <= 3 && 3 <= 5));
```

The above code outputs the following to the console.

```text
3 is between 1 and 5: true
```

### Logical-or Operator

The logical-or operator (`||`) evaluates to `true` if at least one argument is `true`. Below is the truth table for the 
logical-or operator. *A + B* is read as *A or B*.

| A | B | A + B |
|---|---|-------|
| F | F | F     |
| F | T | T     |
| T | F | T     |
| T | T | T     |

We can see that as long as one argument is `true`, the logical-or operator will evaluate to `true`. The following 
code demonstrates using the logical-or operator.

```java
IO.println("3 is greater than 10 or less than zero: %b".formatted(3 > 10 || 3 < 0));
```

The above code outputs the following to the console.

```text
3 is greater than 10 or less than zero: False
```

### Logical-not Operator

The logical-not operator (`!`) evaluates to `true` if its argument is `false`, and vice versa. Below is the truth 
table for the logical-not operator. *~A* is read as *Not A*.

| A | ~A |
|---|----|
| F | T  |
| T | F  |

The logical-not operator inverts the value of its argument. The following code demonstrates using the logical-not 
operator.

```java
final var isHot = true;
IO.println("It's cold outside: %b".formatted(!isHot));
```

The above code outputs the following to the console.

```text
It's cold outside: false
```
