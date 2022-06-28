# **You Need to Learn Regular Expressions Right Now!**

This tutorial will cover Regular Expressions more commonly referred to as "RegEx". To me the most interesting aspect of RegEx is that it can be used in all*¹ programming languages. 
RegEx can be considered a universal language of sorts due to this cross compatibility.<br>
The most common applications for RegEx are Find, replace, and validation of string type data.  

## Summary

This tutorial os sorts will cover probably the most common use case for RegEx and that's email validation. Below is an example of an email validation Regular Expression.↓
<br>
    `/^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6})*$/gm`
<br>
In the following material we will cover what every bit of this wild looking syntax tells the program to do preform. And how to apply it many other scenario.
<br>
<br>


## Table of Contents

- [Lazy and Greedy Match](#lazy-and-greedy-match)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
<br>
<br>


## **Regex Components**
***

<br>
<br>
<br>


### Lazy and Greedy Match
***
<br>

First although it may be difficult to understand just yet we should cover the "Lazy and Greedy" modifiers*².<br>
The ` * ` symbol is known as a 'greedy' modifier. It functions as a 'zero or many' modifier.
<br>

The `.*? ` is know as a 'lazy' modifier. This is used to only match what is necessary to fulfill the giving search parameter. For example `.*?foo` would find one instance of 'foo' and then stop its search as it is now completed. This is also referred to as "Once or none".
<br>
<br>


### Anchors
***
<br>

Anchors are used to match the position of a character. This is useful for determining if a string starts, ends with, is preceded by, or followed by a character(s).
<br>

#### *Examples:*

`^` Is used to find a parameter at the start of a string or line - `^foo.*` <br>
`$` Is used to find a parameter at the end of a string or line - `.*?bar$` <br>
<br>
<br>


### Quantifiers
***
<br>

The `?` and `*` discussed at the beginning of this list are actually quantifiers that were referred to at the time as 'modifiers'.<br>

That information was covered here: [Lazy and Greedy Match](#lazy-and-greedy-match)

In RegEx a quantifier is used to match the quantity of whatever precedes it. For example the syntax `R+` is using the `+` quantifier to 'one or many' letter "R"'s. 
<br>

Next we will look at finding a range using a RegEx. Givin the following RegEx: `X{3,6}` we would here be searching for repeating "XXX"-"XXXXXX" as a range so if in a string you had "XXXX" it would also be included in the results. If you were to leave the last range value blank e.g.: `X{3,}` we would find any string containing "XXX" or more repeating "X" characters. This may sound familiar as it has the same functionality as using the `*` syntax*³ except for the caveat that you gt to specify how many repeating characters it must begin with.
<br>

Now with that in mind we have the following: `X{3,}?`. Here we have a very similar expression it acts as a *lazy* version of the same syntax. So here it would find the instance one time and be complete. 
<br>

Finally we will take a look at this: `X{3}`. In this expression we would be looking for and only for 3 repeating X's. I.E. "XXX" no more and no less.
<br>
<br>


### OR Operator
***
<br>


The "Or" operator works just like it sounds and is represented at the `|` symbol. Most comonly you will see this paired with `( )` to contain an or operator. So this: `(a|b)` would be searching for 'a' or 'b'. And this: `(a|b)c` would find any instance of 'ac' or 'bc'.
<br>

You can get a similar functionality from the square brackets `[ ]`, but with some key differences. First of all the `|` operator is not used with square brackets. To use the previous example with square brackets: `[ab]c` we would be searching for any instance of the letter 'c' preceded by either 'a' or 'b', but would not return 'a' or 'b' with the results. So if we had this string: "aaa babab caca" we would get a result of "c".
<br>
<br>


### Character Classes
***
<br>

Classes are 'words', 'whitespace', 'digits'*⁴, and `'.'` period along with other more specific targets like 'tabs'. <br>

Here we will take a lokk at a few examples:<br>
* `\w` - Is used to identify a 'word'.
* `\d` - Is used to identify a 'digit'.
* `\s` - Is used to find 'whitespace'.
* `\t` - This is how you would find 'tabs'.
* `\v` - And this is how to identify 'vertical whitespace'.
<br>

For example when searching for a word preceded by the letter 'a', here we will use the example "a word". You could wright an expression as such: `a+\s\w` and find the instances of "a word". To get more in depth this would also return 'a ford', 'a cord', ect...
<br>
<br>

 
### Flags
***
<br>

Regular expressions include optional flags that enable features like case-insensitive and global searches. These flags, which are a component of the regular expression, can be used individually or collectively in any combination.
<br>

Some examples:

* `g` - This denotes a Global search.
* `m` - The "m" parameter is for "multi-line searches"
* `i` - Use the 'i' flag to invoke "case-insensitivity"

These flags are used at the end of a regular expression preceded by a forward slash '`/`'. A great example is in our orignal example:<br>  `/^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6})*$/gm` ← Right at the very end we see an example of the flags in use. The `g` flag is using a global search that will look for all matches. Whithout the `g` flag it would only return the first result. Next we have the `m` flag which is using the 'multi-line' mode to be able to match content even if the strings are broken by breaks such as `<br>`. 
<br>
<br>


### Grouping and Capturing
***
<br>

Multiple charactors may be treated as a group by using `( )`. Capture groups have several configuations:
* `(X)`
* `(X(Y))`
* `(foo(X(Y)))`
<br>

Our example expression at the top of the page has our RegEx in it's own capture group. The outer expressions dictate where to look for our combination of email validation expressions.
<br>
<br>

### Bracket Expressions
***
<br>

In RegEx we use square brackets `[]` to identify a list of characters.
<br>

Take the following example: `[XYZ]`.← This expression would find any instance of the uppercase 'X', 'Y', or 'Z' treating what's contained in the square brackets as a list. This method can be extremely useful when looking for a character that would normally dictate a regular expression itself. In this example→ `[^?${}[()]` we can see a lot of syntax that would normally trigger a regular expression, but here it gives us the ability to find these characters in a string or document.  
<br>

Another common method used with square brackets is when searching for characters within a range. 
<br>

In this example→ `[A-Za-z0-9]` we are looking for all the upper and lowercase letters in the english alphabet and any number 0-9.
<br>
<br>

### Boundaries
***
<br>

We are going to take a look at a different but related example for the topic of boundries. For this we are going to look at years.↓
<br>

    1999-06-14
    1996.12.21
    1864 08 04
    2022/01/01
<br>

Now say we just want the years from these dates one method we could use is a boundary→ `\b`. A simple way for find just the year would be wit the following example→ `\b\d\d\d\d\b` remember that `\d` is searching for a *digit* and the `\b` is a boundary. In this instance it would return "1999, 1996, 1864, and 2022" as whitespace, periods, slashes, and hyphens are all considered boundary characters.
<br>
<br>

### Back-references
***
<br>

A great use case for back-references is any time you may be searching for a double word. For example→ "I may 'not not' have this figured out." We could use a combination of what we have learnered so far and apply it to a back referance. 
<br>

To  find the doubling of 'not not' in our above sentence we would use something like this→ `\b(w+)\s\1\b`. So let's break thins down a bit and see whats going on here. First we create our boundaries→ `\b\b` then we know we are looking for two words divided by a whitespace so lets add that→ `\b\s\b`. Next we will want to search for any word, but we will want to contain it for back-reference and look for 'one or many' words in a row, so lets add that next→ `\b(w+)\s\b`. Now we are ready to use our back-reference. We created a group when we added `(w+)` to our RegEx that is *group 1* and how we will reference it in our expression→ `\b(w+)\s\1\b`. What we added here is the `\1` to the expression in reference the first group. If we had more groups in our expression the could be represented as follows→ `\1`, `\2`, `\3`,... So the result of this expression when searching our test sentence would return "not not".
<br>
<br>

### Look-ahead and Look-behind
***
<br>

The last thing we are going to talk about is looking ahead and behind. To look ahead we use `Y(?=X)`*⁵, and to look behind we use `Y(?<=X)`. So if we wanted to match 'Y', but only if it's followed by 'X' we would use `Y(?=X)`, Inversly if we want to find 'Y', but only if it is preceded by 'X', we would use the look-behind→ `Y(?<=X)`.

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)

<br>
<br>
<br>
<br>
<br>
<br>
<br>

#### Footnotes 
***

  *¹ *Supported by most mainstream programming languages.*<br>
  *² *Modifier in this instance is interchangeable for quantifier.* <br>
  *³ *Greedy*<br>
  *⁴ *Numbers or Integers*<br>
  *⁵ *the 'X', and 'Y' are not part of the expression they are just placeholder values.*

