# Mastering Regular Expressions

by Josef Fridl

# Chapter 1 - Introduction to Regular Expressions


### 1.4.2 Character Classes

Almost like their own mini language and have their own metacharacters → _character-class metacharacters_

| | |
|-|-|
| Range                     | `q[a-zA-T0-9]` |
| Not a Range               | `q[-u]`        |
| Negated character classes | `q[^u]`        |

The last one would be read as _"q followed by a character that's not **u**"_

_'A negated character class is simply a notational convenience for a normalcharacter class that matches everything not listed. Thus, `[^x]` doesn't  mean "match unless there is an x", but rather "match if there is something that is not x".   The difference is subtle, but important. The first concept matches a blank line, for example, while `[^x]` does not.'_ - (p 17).


Some useful shorthands:

| Shorthand              | Equivalent                |
| ---------------------- | ------------------------- |
| `\d`                   | `[0-9]`                   |
| `\w` (word char)       | `[A-Za-z0-9_]`            |
| `\s` (whitespace char) | `[\t\r\n\f]` <sup>1</sup> |

1) dependent on RE engine.

### 1.4.4 Alternation |

Matching any one of several subexpressions. Part of the "main" RE language.

  - each alternative can be a full-fledged regular expression in and of itself.
  - parentheses "constrain" the alternation.
  
_'Don't confuse altneration with a character class [...] A character class can match exactly one character [...] Alternation, on the other hand, can have arbitrarily long alternatices, each tectually unrelated to the other.'_
  
### 1.4.5 Ignoring Differences in Capitalization
  
It is not a part of the regular-expression language, but is a related useful feature many tools provide.

E.g. _egrep's_ command-line option `-i` tells it to do a case-insensitive match. Place `-i` on the command line before the regular expression.

### 1.4.8 Optional Items

'?' - _'placed after the optional character that is allowed to appear at that point in the expression, but whose existence isn't actually required to still be considered a successful match.'_ - (p 17)

_'Unlike other metacharacters we have seen so far, the question mark attaches only to the immediately-preceding item.'_

'?' can attach to a parenthasized expression. Inside the parentheses can be as complex a subexpression as you like, from outside it is considered a single unit.

Grouping for '?' (and other similar meta characters) is one of the main uses of parentheses.

### 1.4.9 Other Quantifiers: Repetion

'+' -> "one or more of the immediately preceding item
'*' -> "any number, including none, of the item", or, "try to match it as many times as possible, but it's OK to settle for nothing if need be"

Note that each quantifier has some minimum number of matches required to succeed, and a maximum number if matches that it will ever attempt.

Some versions of egrep support a metasequence for providing your own min/max: `{min,max}`, aka _interval_ quantifier.

### 1.4.10 Parentheses and Backreferences

In many RE flavours, parentheses can "remember" text matched by the subexpression they enclose. It is a feature that allows you to match new text that is the same as some text matched earlier in the expression.

Be aware that some versions of egrep, including older versions of popular GNU offering, have a bug with the `-i` option such that it doesn't apply to backreferences.

### 1.4.11 The Great Escape

`\.` - Match a dot, not any character

A backslash used in this way is called an "escape" - when a metacharacter is escaped, it loses its special meaning and becomes a literal character.

When used before a non-metacharacter, a backslash can have different meanings depending upon the version of the program. These can be called metasequences, e.g. `\<` and `\>` (word boundaries) and `\1` (back-reference).

## 1.5 Expanding the Foundation

1.5.1 Linguistic Diversification

There are various dialexts and accents. It seems that each new program employing RE devises its own "improvements". The state of the art continually moves forward, but changes over the years have resulted in a wide variety of regular expression "flavours".

1.5.2 The Goal of a Regular Expression

When crafting a regular expression, you must consider the ongoing tug-of-war between having your expression match the lines you want, yet still not matching the lines you don't want.

If your intent is to do something with a match, which is quite common (such as find/replace), then you very much care where the match occurs.
