# Regular Expressions

Regular Expressions, or RegEx, are helpful tools used across many programming languages to find a specified combination of characters.  A RegEx allows the programmer to search for any variation of a string matching a pattern instead of being limited to a specific, or "literal", query.  For example, in a large database with multiple email address entries, a RegEx pattern search of `[any name]@[any domain].[any extension]` will easily find all email addresses.

In addition to being powerful search tools, regular expressions can be applied to validate formatting (e.g. passwords and email address), perform quick replacements, and assist with string splitting.

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors
Anchors are special characters that identify the position of the searched text.  A caret (`^`) anchor identifies the beginning of a string while a dollar sign (`$`) identifies the end of a string.  A word boundary anchor (`\b`) is used to identify the beginning or end of a word.  Without anchors, the RegEx will search for the identified pattern within any position of a given string. 

### Quantifiers
Finally, quantifiers identify how the number of occurrences of the preceeding characters from either the literal character or character set.  Our email RegEx uses a plus (`+`) and brace (`{...}`) quantifiers, as seen here: `([...]+)@([...]+)\.([...]{2,6})`.  The presence of the plus signifies a match for any of the characters found in the preceeding bracket expression at least one time.  The brace specifies a range of matches from `2` to `6` of the characters found in the preceeding bracket expression.
#### Example
A RegEx search of `/[a-z\d]{2, 8}@email\.com/` will match the email "l33tc0de@email.com" but not "ilove2code@email.com".  The local-part of the latter is ten characters in length and does not meet the quantifier requirements.

### OR Operator

### Character Classes
In our above bracket expressions, the following character sets are used:
| Character Class | Meaning |
| ----------- | ----------- |
| `a-z` | Match any letter within the range of lowercase a to lowercase z. |
| `0-9` | Match any number from 0 to 9. |
| `_` | Match literal underscores. |
| `\.` | Match literals dot (`.`).  Dots have special functions in regular expression.  The backslash (`\`) is used to escape the character. |
| `-` | Match literal hyphens. |
| `\d` | Match any digit from 0 to 9.  Effectively the same as using `0-9`. |
| `@` | Match literal at signs.  Found following the first parenthetical group in our email RegEx. |

#### Example
A RegEx search of `/\b[a-z]{4}\b/` on the string "today's date is 2/26" will match the word four-letter word "date".  Although "2/26" is also a four-character string within the appropriate word boundaries, it contains characters that are not included in `a-z`.
### Flags

### Grouping and Capturing
After removing our anchors from our email RegEx, we are left with the following.
```
([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})
```
Note that there are three sets of parentheses in this regular expression: `(...)@(...)\.(...)` where the  `...` replaces expressions we will discuss later.

Parentheses do not affect the results of the search pattern, but instead group and capture sections of the pattern together.  By default, the entire string is Group 0.  Each subsequent parenthetical captured group is Group 1, Group 2, Group 3, etc.  Captured groups can then be referenced as needed.
### Bracket Expressions
Next in our email RegEx, we have three sets of bracket expressions.  Simply put, a bracket expression contains a list of characters enclosed in brackets (`[` and `]`).  This will perform a search of any character found within this list.  However, if the bracket expression begins with a caret (`^`), then the search will **exclude** all characters from that list.

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

This gist was written by Kruti Patel, a forensic investigator turned full-stack developer.  To see more of kruti's work, please visit her [GitHub](https://github.com/krutipatel07).