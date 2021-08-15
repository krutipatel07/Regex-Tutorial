# Regular Expressions

Regular Expressions, or RegEx, are helpful tools used across many programming languages to find a specified combination of characters.  A RegEx allows the programmer to search for any variation of a string matching a pattern instead of being limited to a specific, or "literal", query.  For example, in a large database with multiple email address entries, a RegEx pattern search of `[any name]@[any domain].[any extension]` will easily find all email addresses.

In addition to being powerful search tools, regular expressions can be applied to validate formatting (e.g. passwords and email address), perform quick replacements, and assist with string splitting.

## Summary

In this gist, we will introduce JavaScript regular expressions using the following RegEx for matching an email address.
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
We will dissect the above RegEx into components and elaborate on each.

## Table of Contents
- [Anchors and Boundaries](#anchors-and-boundaries)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [Quantifiers](#quantifiers)
- [Conclusion](#conclusion)
- [Author](#author)

## Regex Components

### Anchors and Boundaries
In our regular expression for matching an email address, we have surrounded our RegEx search with the anchors `^` and `$` to identify that the enclosed search pattern should not have any other characters, including spaces, before or after it.  It should also be noted that all regular expression searches begin and end with a forward slash (`/`).

Anchors are special characters that identify the position of the searched text.  A caret (`^`) anchor identifies the beginning of a string while a dollar sign (`$`) identifies the end of a string.  A word boundary anchor (`\b`) is used to identify the beginning or end of a word.  Without anchors, the RegEx will search for the identified pattern within any position of a given string.

#### Example
A RegEx search of `/hat/` on "that hat" will return "t***hat*** ***hat***" with both instances of the letter combination "hat" because it does not discriminate the positioning within the string.  A search of `/hat$/` will find "that ***hat***," matching only the "hat" located at the end of the string.  Additionally, `/^hat/` will return no matches, as there are no instances of the pattern "hat" located at the beginning of a string.  Finally, to locate only instances of the word "hat," enclose the RegEx search in word boundaries (`/\bhat\b/`).

### Grouping and Capturing
After removing our anchors from our email RegEx, we are left with the following.
```
([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})
```
Note that there are three sets of parentheses in this regular expression: `(...)@(...)\.(...)` where the  `...` replaces expressions we will discuss later.

Parentheses do not affect the results of the search pattern, but instead group and capture sections of the pattern together.  By default, the entire string is Group 0.  Each subsequent parenthetical captured group is Group 1, Group 2, Group 3, etc.  Captured groups can then be referenced as needed.

#### Example
In the following example, we will use our email RegEx, assigned to the `re` variable, on the email address "johndoe@email.com," assigned in the `email` variable.  We can then refer to specific groups within our email address as needed.
```
const email = 'johndoe@email.com'
const re = email.match(/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/)

console.log(re[0]) //=> prints "johndoe@email.com"
console.log(re[1]) //=> prints "johndoe"
console.log(re[2]) //=> prints "email"
console.log(re[3]) //=> prints "com"
```
As you may have noticed, this looks similar to referencing an array, and that's because it is!  Running `console.log(re)` would print an array of `['johndoe@email.com', 'johndoe', 'email', 'com']`.

### Bracket Expressions
Next in our email RegEx, we have three sets of bracket expressions.  Simply put, a bracket expression contains a list of characters enclosed in brackets (`[` and `]`).  This will perform a search of any character found within this list.  However, if the bracket expression begins with a caret (`^`), then the search will **exclude** all characters from that list.

#### Example
Our RegEx contains three bracket expressions: `[a-z0-9_\.-]`, `[\da-z\.-]`, and `[a-z\.]`.  The character lists will be explained further in the next section.

### Character Classes
Character classes identify the set of characters to be matched and are often, but not exclusively, used in conjunction with bracket expressions.

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

### Quantifiers
Finally, quantifiers identify how the number of occurrences of the preceeding characters from either the literal character or character set.  Our email RegEx uses a plus (`+`) and brace (`{...}`) quantifiers, as seen here: `([...]+)@([...]+)\.([...]{2,6})`.  The presence of the plus signifies a match for any of the characters found in the preceeding bracket expression at least one time.  The brace specifies a range of matches from `2` to `6` of the characters found in the preceeding bracket expression.

#### Example
A RegEx search of `/[a-z\d]{2, 8}@email\.com/` will match the email "l33tc0de@email.com" but not "ilove2code@email.com".  The local-part of the latter is ten characters in length and does not meet the quantifier requirements.

### Conclusion
Now that we've dissected our email RegEx, let's put it back together and evaluate what our match might look like.  Recall that the original RegEx is as follows.
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
This regular expression will match a string containing a combination of **one or more** characters consisting of...

- any *lowercase* letters from a-z
- any digit from 0-9
- underscores
- dots, or
- hyphens

... followed by a *literal* `@`, followed by a combination of **one or more** characters consisting of...

- any digit from 0-9
- any *lowercase* letters from a-z
- dots, or
- hyphens

... followed by a *literal* `.`, followed by a combination of **two to six** characters consisting of...

- any *lowercase* letters from a-z, or
- dots

The match also cannot have *any* characters preceeding or following it, including spaces.

That was a lot!  And there is still plenty more to explore with RegEx, including greedy and lazy matches, look-aheads and look-behinds, and other special characters not discussed here.  For more information on regular expressions, check out [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)!

## Author

This gist was written by Kruti Patel, a lazy girl turned full-stack developer.  To see more of kruti's work, please visit her [GitHub](https://github.com/krutipatel07).