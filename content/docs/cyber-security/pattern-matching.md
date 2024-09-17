---
title: "1.3. Pattern Matching"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.3. Pattern Matching

Pattern matching is where strings of text are found using a **regular expressions**. Without **regular expressions**, **keyword searching** would have to be used.

## Keyword Searching

Keyword searching is where strings of text are found by using keywords, much like a Google search works. This is limited in many circumstances, such as:

- `Dave` will match `Dave` but not `David`
- `192.168.0.0` will match only `192.168.0.0` but not `192.168.10.2`

## Regular Expressions

A regular expression (regex) is are more sophisticated version of keyword searching, where special characters, known as 
**metacharacters** are used.

Regular expressions are made of **atoms**, **metacharacters**, and **operators**.

**Atoms** are the most basic part of regex, and is simply just a set of characters to match.

Regular expressions can be used with commands built-in to Linux/Unix, such as: `grep`, `egrep`, `sed`, `awk`, and **Python**.

| Metacharacter | Matches |
|:-------------:|:--------|
| `.` | Any one character, except a new line |
| `[a-z]` | Any one of the enclosed characters |
| `*` | **Zero or more** of the preceding character |
| `?` | **Zero or one** of the preceding character |
| `+` | **One or more** of the preceding character |
| `^` | Beginning of the line |
| `$` | End of the line |
| `\` | Escape character |
| `[^]` | One character **not** in the set |
| `\d` | Digit (0-9) |
| `\D` | Not a digit (0-9) |
| `\w` | Word character (a-z, A-Z, 0-9, _) |
| `\W` | Not a word character |
| `\s` | Whitespace (space, tab, new line) |
| `\S` | Not whitespace |
| `\b` | Word boundary |
| `\B` | Not a word bounday |

Examples of regular expressions:

- `^hello`: Line begins with `hello`
- `hello$`: Line ends with `hello`
- `colou?r`: Matches `color` and `colour`

### Class Matching

Matches a single character that is defined in a set.

- `[ABC]` matches either `A`, `B`, or `C`
- `[C-E]` matches either `C`, `D`, or `E`

Shorthand classes can be used to quickly define sets.

| Shorthand | Description |
|:---------:|:------------|
| `[:alnum:]` | Matches alphanumeric characters |
| `[:alpha:]` | Matches alphabetic characters |
| `[:upper:]` | Matches uppercase letters |
| `[:lower:]` | Matches lowercase letters |
| `[:digit:]` | Matches digits |
| `[:space:]` | Matches whitespace characters, including new line |

### Operators

Regular expressions rely on **operators** to build advanced queries. Operators are used in between **atoms**, sililar to **metacharacters**.

#### Sequence Operator

By default, having no symbol between atoms is known as the **sequence** operator. For example: `cat` matches the pattern `cat`.

#### Alternation Operator (`|`)

**Alternation** is pretty much an OR in programming.

- `Unix|Linux` will match `Unix` or `Linux`.

#### Repetition Operator (`{...}`)

Specifies the atom before the operator is repeated.

- `BA{3,5}` matches `BAAA`, `BAAAA`, or `BAAAAA`.

Shorthands can also be used:

- `{n}`: Matches previous atom exactly `n` times
- `{n, }`: Matches previous atom `n` times or more
- `{, n}`: Matches previous atom `n` times or less

#### Group Operator (`(...)`)

Signals that the next operator applies to the while group, not just the previous characters.

- `A(BC){3}` matches `ABCBCBC`.

For the keyword searching limitations above:

- `Dav(e|id)` will match `Dave` and `David`
- `192\.168\.([:digit:]{1,3})\.([:digit:]{1,3})` will match `192.168.0.0` and `192.168.10.2`
    - Note the use of **escape operators** `\`, and the **repetition operator**.

For more information on regular expressions, see [RegExr](https://regexr.com/), [Cyrilex](https://extendsclass.com/regex-tester.html) and [Regular-Expressions.info](https://www.regular-expressions.info/).
