# What is "Regex"?

## Regular Expressions:

Regular Expressions, or Regex for short, is an object that describes a pattern of charachters used to search through a given string and extract specific elements. These charachters could be anything from letters, numbers to white-space. 

With Regex you can create specific patterns to search through, find, or/and replace any character combination in the string, i.e check a valid email is input, remove phone numbers from a text body or just validate a password. Regex gives you the flexibily and freedom to define your own search criteria and create a pattern that fits the needs for to solve your task. 



### Syntax

As an example lets have a look at a few differnt types of Regex patterns created to carry out a specific job.

```
Syntax: /pattern/flags;

* Matching a Hex Value: `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/`

* Matching an Email: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

* Matching a URL: `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

* Matching an HTML Tag: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

```

In this tutorial I will looking at the matching email example and deep dive into it and breaking it down into its components to explain what each part of the pattern means.


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

* **Caret: ^**  Matches the following regex at the beginning of a string
* **Dollar Sign: $**  Matches the preceding regex at the end of a string

Anchorse are used to test if a string fully matches the pattern created in your regex. It's important to note that anchors do not actually match a character but force the regex pattern to check the entire string for a match. If you look at the example below you can see that email pattern is wrapped in between the two anchors.

* Matching an Email: 

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```


### Quantifiers
* Quantifirs are essentially numbers wrapped in curly brackets {n}. Their purpose is to specify how many of a character we need.

* Matching an Email: 
* From our we example we can see that it has a 'range' quantifier of {2, 6} which tells us that this particular pattern should be matched 2-6 times.

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

Other Quantifiers to note are:

* **`*`**	Match zero or more times.
* **`+`**	Match one or more times.
* **`?`**	Match zero or one time.
* **`{ n }`**	Match exactly n times.
* **`{ n ,}`**	Match at least n times.
* **`{ n , m }`**	Match from n to m times.

### Grouping Constructs

Grouping Constructs or Capturing groups are a way to break down a regex pattern into seperate groups by enclosing them with parenthesis (...).


* Matching an Email: 
* Lets look at our email example, we can clearly see that there are 3 groups.
* if we look at how emails are constructed  `username` **`@`** `domain` **`.`** `com`  we see that the grouping structure follows this pattern.


```
/^
```
* The first part `username` tells us that any letter and number comnination including **`_ - .`** can be used.
```
([a-z0-9_\.-]+)
```
* This tells us that the first part needs to be followed by `@` symbol.
```
@
```
* The second part again like the first tells us that the `domain` can be any character combinations 
```
([a-z0-9_\.-]+)
```
* This tells us that the second part needs to be followed by `.` symbol.
```
.
```
* The 3rd part unklike the top 2 parts tell us, that the `suffix` can only contain letters and a dot '.' and can only be between 2 - 6 characters long.
```
([a-z\.]{2,6})
```

```
$/
```

### Bracket Expressions
`[]` Square Brackets in Regex are used to match or unmatch any characters between them. 
```
[a-z\.]
```

`{}` Curly Brackets are used to specify an exact amount of things to match. (quantifiers)
```
{2,6}
```

`()` Parenthesis represent groups in your regex code. (groupoing constructs)
```
([a-z\.]{2,6})
```


### Character Classes
Character classes are specical notations that help us to distinguish between characters. this allows us find or remove any characters including white spaces in a string.

* They are oftern written with a `\` followed by a specific `letter`. 

Example Character Classes below:
* `\d` – digits.
* `\D` – non-digits.
* `\s` – space symbols, tabs, newlines.
* `\S` – all but \s.
* `\w` – Latin letters, digits, underscore '_'.
* `\W` – all but \w.
* `\.` - A dot .  matches any character except a newline.


```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
We can see in our email regex that the `\.` character class is used.

### The OR Operator



### Flags

In simple terms Flags are 'optional' parameters added to the end of an expresion allowing you to be able to modify the search behaviour of your expressions.

There are multiple types of flags each denoted by an alphabetic character with each one serving a different purpose in modifying how your expression searchs through the 'text'.

Flags are placed after the second slash in your Regex: `/pattern/flags`. It is also important to note that you can also chain flags together, i.e `/pattern/ig`.  Below are examples of the differnt types of flags available for you to utilise.


**Ignore Casing: /pattern/`i`:**
* the `i` flag allows you to ignore letter casing, allowing to search any form of a string regardless of your pattern being wrtiten in upper or lowercase.

* i.e /helloworld/i will find HelloWorld, HELLOworld, HELLOWORlD

**Global: /pattern/`g`**

* the `g` flag allows you to search all occurances of a pattern rather than just the first.

**Dot ALL:  /pattern/`s`**
*  The “dotall” flag allows a dot `.` to match a newline character \n. the dot `.` itself acts as a special charachter that matches any character except a newline. 


**Multiline: /pattern/`m`**

* Makes the boundary characters `^`(start) and `$`(end) match the beginning and ending of each line rather than just the start and end of the whole string.

**Sticky: /pattern/`y`**

* The `y` flag allows you to perform a search at a given position in a string, usually from the point stored in the .lastIndex property.


### Character Escapes



In Regex, There are many special characters that have special meanings and are often used used to do more powerful searches. 

In order to use these characters we need to append them to a  backslash `\`. 'Escape them'.

this backslash `\` is what is know as an escaping character.


Here is a list special characters that can be 'escaped with a backslash: `[ \ ^ $ . | ? * + ( )`.


```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
* You can see that our email regex has 4 character escape.

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
