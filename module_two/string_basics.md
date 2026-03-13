# Strings

## String Literals

### Basic String Literals

Enclosing text in double quotes creates a *string literal*. String literals can then be assigned to variables to 
create `String` objects. The following code demonstrates creating a string from a string literal.

```java
final var sentence = "Hello, world!";
```

#### Escape Sequences

We can also include *escape characters* in string literals. Escape characters are characters formed by escaping 
another character with the *escape character* (`\`). We can use these escape characters to include newlines and tabs in
strings, among other things. The following code demonstrates using escape characters for newline (`\n`) and tab (`\t`).

```java
IO.println("\tEach\nword\nwill\nbe\non\nits\nown\nline");
```

The above code outputs the following to the console.

```text
    Each
word
will
be
on
its
own
line
```

We can also use the escape character to help us output characters we would otherwise have trouble with. For example, 
you can't normally output a double quote since Java would treat it as the end of the string literal. A similar problem
exists when trying to write a backslash character in a string literal since backslash is the escape character. The
following code demonstrates how we can output double quotes and backslashes using escape characters.

```java
IO.println("Here is a \"backslash\": \\");
```

The above code outputs the following to the console.

```
Here is a "backslash": \
```

### Text Blocks

Sometimes we want to write strings which would end up spanning multiple lines in the console. This means we would 
need to include a lot of newline characters, which would make it a bit hard to read the string. This is where *text 
blocks* come in! These string literals will ignore all escape sequences, meaning backslashes will work just fine 
without escaping. Text blocks also let us span multiple lines, and any formatting in a text block becomes part of the 
final string! This means if we indent in a text block, the indentation will be in the actual string! The following code 
demonstrates creating a string from a text block.

```java
final var dialog = """
    It was time to write some code.
        "Hello, world!" said the code.
        "Goodbye, code!" said the programmer, fearing his creation had
    become sentient.""";
IO.println(dialog);
```

The above code outputs the following to the console.

```text
It was time to write some code.
    "Hello, world!" said the code.
    "Goodbye, code!" said the programmer, fearing his creation had
become sentient.
```

Notice how the formatting is remembered by the string and now none of the double quotes needed escaping? This is the 
power of text blocks! Definitely make use of them when you need a string that spans multiple lines.

When declaring a text block, the opening triple double quotes must be on their own line. The closing triple double 
should go at the end of the last line unless you want newlines at the end of the text block.

## String Methods

### Parsing Helpers

It's often desirable to get rid of stray whitespace around a string when we need to parse it. Java strings have a 
`strip` method which strips leading and trailing whitespace characters.

```java
final String input = IO.readln("Enter a word: ").strip();
IO.println("Your input was \"%s\"".formatted(input));
```

The above code outputs the following to the console.

```text
Enter something:         okay      
You entered: "okay"
```

It's also possible to convert a string to all uppercase or all lowercase. These methods can be helpful when it's not 
possible to perform case-insensitive comparisons in the traditional way.

```java
final String word = IO.readln("Enter a word: ");
IO.println(word.toLowerCase());
IO.println(word.toUpperCase());
```

The above code outputs the following to the console.

```text
Enter a word: Hello
hello
HELLO
```

### Concatenation

*Concatenation* is when we combine multiple strings into one string. To concatenate strings, we use the *addition 
operator* (`+`).

```java
final String word1 = IO.readln("Enter a word: ");
final String word2 = IO.readln("Enter another word: ");
IO.println(word1 + word2);
```

The above code outputs the following to the console.

```text
Enter a word: hello
Enter another word: world
helloworld
```

Concatenation is useful when we want to simply combine two or more strings. If we want to build a string from many 
different values, or if we want to combine a string literal and a value for outputting, it's better to use a formatted 
string.

### `length` and `charAt` Methods

If we want to get the length of a string (i.e., the number of Unicode characters), we can use the `length` method.

If we want to get a character at a particular index value, we can use the `charAt` method.

The following code demonstrates the `length` and `charAt` methods.

```java
final var word = "hello";
IO.println("%s has %d character(s) in it!".formatted(word, word.length()));
IO.println("%s starts with the letter %c".formatted(word, word.charAt(0)));
```

What if we wanted to get the last letter in word? We could combine the `length` method with the `charAt` method!

```java
IO.println("%s ends with the letter %c".formatted(word, word.charAt(word.length() - 1)));
```

Unfortunately, Java has no way of neatly getting the last character in a string. The Java developers debated adding a 
feature to support this, but they ultimately decided against it.

### Substrings

If we want to get a substring, we can use the `substring` method. This method can take either one or two arguments. 
Providing one argument gets you a substring starting from the character at the provided index value and going to the 
end of the string. Providing two arguments gets you a substring starting from the character at the first index value 
and going to the character one before the second index value. The following code demonstrates getting different 
substrings.

```java
final var word = "hello";
IO.println(word.substring(1, 4));
IO.println(word.substring(0, 3));
IO.println(word.substring(2));
```

The above code outputs the following to the console.

```text
ell
hel
llo
```

### Inclusion

#### `contains` Method

If we want to check if a string contains a particular character or substring, we can use the `contains` method. This 
method checks if a string contains a particular character sequence. This check is always case-sensitive, meaning asking 
if a string contains "A" versus "a" are different questions.

```java
final var word = "Apple";
IO.println(word.contains("a"));
IO.println(word.contains("A");
```

The above code outputs the following to the console.

```text
false
true
```

#### `indexOf` and `lastIndexOf` Methods

If we want to get the index value of the first occurrence of a particular character or substring, we can use the 
`indexOf` method. We could also get the index value of the last occurrence of a particular character or substring using 
the `lastIndexOf` method. These methods are also always case-sensitive. The following code demonstrates this.

```java
final var word = "apple";
IO.println("First occurrence of 'p': %d".formatted(word.indexOf('p')));
IO.println("First occurrence of 'P': %d".formatted(word.indexOf('P')));
IO.println("Last occurrence of 'p': %d".formatted(word.lastIndexOf('p')));
IO.println("First occurrence of \"app\": %d".formatted(word.indexOf("app")));
```

The above code outputs the following to the console.

```text
First occurrence of 'p': 1
First occurrence of 'P': -1
Last occurrence of 'p': 2
First occurrence of "app": 0
```

When checking for the index of a substring, the returned value will be the index value of the first character in the 
substring. If there are no occurrences of a character or substring, -1 is returned.

Sometimes we want to find additional occurrences of characters or substrings after the first occurrence. We can do this 
by providing the `indexOf` method with a starting index value so it will only find occurrences from that index value to 
the end of the string. This also works for the `lastIndexOf` method. The following code demonstrates this.

```java
final var word = "apple";
int indexOfFirstP = word.indexOf('p');
int indexOfSecondP = word.indexOf('p', indexOfFirstP + 1);
int indexOfFirstL = word.lastIndexOf('l');
int indexOfSecondL = word.lastIndexOf('l', indexOfFirstL - 1);
IO.println("Index values of 'p': %d, %d".formatted(indexOfFirstP, indexOfSecondP));
IO.println("Index values of 'l': %d, %d".formatted(indexOfFirstL, indexOfSecondL));
```

The above code outputs the following to the console.

```text
Index values of 'p': 1, 2
Index values of 'l': 3, -1
```

Additionally, we can provide an ending index value for where the search should stop. While the starting index value is 
inclusive, the ending index value is *exclusive*. The `lastIndexOf` method doesn't support this extra argument.

```java
final var phrase = "appleapple";
IO.println("Index of \"ea\": %d".formatted(phrase.indexOf("ea", 0, 5)));
IO.println("Index of \"ea\": %d".formatted(phrase.indexOf("ea", 0, 6)));
```

The above code outputs the following to the console.

```text
Index of "ea": -1
Index of "ea": 4
```

The first call to `indexOf` returns -1 since there is no "ea" between index 0 and index 4. When the search area is 
increased by one character, (i.e., the search area is now index 0 to index 5), the `indexOf` method returns 4 since 
this is the index value of the start of the substring "ea".

### Equality

If we want to check if two strings are equal, we use the `equals` method. We'll discuss why we don't compare strings 
with the *equality operator* (`==`) later, so for now, just know that strings are different. If we want to check if two 
strings are equal without worrying about case, we can perform a case-insensitive search using the `equalsIgnoreCase` 
method. The following code demonstrates both these methods.

```java
final var word1 = "apple";
final var word2 = "APPLE";
IO.println(word1.equals(word2));
IO.println(word1.equalsIgnoreCase(word2));
```

The above code outputs the following to the console.

```text
false
true
```

### Ordering

If we want to see how one string compares to another, we can use the `compareTo` method to do a case-sensitive 
comparison, or the `compareToIgnoreCase` method to do a case-insensitive comparison.

When comparing strings for ordering, Java will compare them *lexicographically*. This means they will be compared for 
their alphabetical ordering. The `compareTo` methods will return a negative number if the first string comes first in 
the alphabet, a positive number if the first string comes second in the alphabet, and a zero if they're the same 
word. The following code demonstrates using the `compareTo` methods.

```java
final var word1 = "apple";
final var word2 = "banana";
final var word3 = "APPLE";
IO.println(word1.compareTo(word2));
IO.println(word1.compareTo(word3));
IO.println(word1.compareToIgnoreCase(word2));
IO.println(word1.compareToIgnoreCase(word3));
```

The above code outputs the following to the console.

```text
-1
32
-1
0
```

The first -1 is because "apple" comes before "banana" in the alphabet, and there is a one-letter difference. The 32 is 
because the comparison was case-sensitive and 'A' comes before 'a' in the Unicode specification. Specifically, 'A' is 
32 letters before 'a'. The second -1 is because changing the case sensitivity doesn't change the result since the 
strings were lowercase already. The 0 is because the comparison was made case insensitive.

## String Immutability

Strings in Java are *immutable*. This means they can't be changed once created. Even though a lot of string methods in 
Java seem like they modify a string, they actually create a copy with the modified property and return that. This is 
important to know because it can affect the performance of your code. We'll learn a big consequence of this in a later 
module.
