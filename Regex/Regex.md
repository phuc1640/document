# Regex

# What is Regex

A regular expression (shortened as regex or regexp also referred to as rational expression) is a sequence of characters that specifies a search pattern. Usually such patterns are used by string-searching algorithms for "find" or "find and replace" operations on strings, or for input validation. It is a technique developed in theoretical computer science and formal language theory.

# Need to know concept
1. Consume

Move the pointer for every characters matched.

2. Greedy

Will try to match as much as possible with the given condition.

# Special characters
`.`

(Dot.) This matches any character.

`^`

(Caret.) Matches the start of the string.

`$`

Matches the end of the string or just before the newline at the end of the string.

`*`

Causes the resulting RE to match 0 or more repetitions of the preceding RE, as many repetitions as are possible. ab* will match `a`, `ab`, or `a` followed by any number of `b`s.(Greedy)

`+`

Causes the resulting RE to match 1 or more repetitions of the preceding RE. ab+ will match `a` followed by any non-zero number of `b`s; it will not match just `a`.(Greedy)

`+`

Causes the resulting RE to match 0 or 1 repetitions of the preceding RE. ab? will match either `a` or `ab`.(Greedy)

`*?, +?, ??`

The `*`, `+`, and `?` qualifiers are all greedy; they match as much text as possible. Sometimes this behaviour isn’t desired; if the RE `<.*>` is matched against `<a> b <c>`, it will match the entire string, and not just `<a>`. Adding ? after the qualifier makes it perform the match in non-greedy or minimal fashion; as few characters as possible will be matched. Using the RE `<.*?>` will match only `<a>`.

`{m}`

Specifies that exactly m copies of the previous RE should be matched; fewer matches cause the entire RE not to match. For example, `a{6}` will match exactly six `a` characters, but not five.

`{m,n}`

Causes the resulting RE to match from m to n repetitions of the preceding RE, attempting to match as many repetitions as possible. For example, `a{3,5}` will match from 3 to 5 `a` characters. Omitting m specifies a lower bound of zero, and omitting n specifies an infinite upper bound. As an example, `a{4,}b` will match `aaaab` or a thousand `a` characters followed by a `b`, but not `aaab`. The comma may not be omitted or the modifier would be confused with the previously described form.(Greedy)

`{m,n}?`

Causes the resulting RE to match from m to n repetitions of the preceding RE, attempting to match as few repetitions as possible. This is the non-greedy version of the previous qualifier. For example, on the 6-character string `aaaaaa`, `a{3,5}` will match 5 `a` characters, while a`{3,5}?` will only match 3 characters.

`\`

Either escapes special characters (permitting you to match characters like `*`, `?`, and so forth), or signals a special sequence; special sequences are discussed below.

`[]`

Used to indicate a set of characters. In a set:

* Characters can be listed individually, e.g. `[amk]` will match `a`, `m`, or `k`.
* Ranges of characters can be indicated by giving two characters and separating them by a `-`, for example `[a-z]` will match any lowercase ASCII letter, `[0-5][0-9]` will match all the two-digits numbers from 00 to 59, and `[0-9A-Fa-f]` will match any hexadecimal digit. If - is escaped (e.g.` [a\-z]`) or if it’s placed as the first or last character (e.g. `[-a]` or `[a-]`), it will match a literal `-`.
* Special characters lose their special meaning inside sets. For example, 1 will match any of the literal characters `(`, `+`, `*`, or `)`.
* Character classes such as `\w` or `\S` (defined below) are also accepted inside a set.
* Characters that are not within a range can be matched by complementing the set. If the first character of the set is `^`, all the characters that are not in the set will be matched. For example, `[^5]` will match any character except `5`, and `[^^]` will match any character except `^`. `^` has no special meaning if it’s not the first character in the set.
* To match a literal `]` inside a set, precede it with a backslash, or place it at the beginning of the set. For example, both `[()[\]{}]` and `[]()[{}]` will both match a parenthesis.

`|`

`A|B`, where A and B can be arbitrary REs, creates a regular expression that will match either A or B. An arbitrary number of REs can be separated by the `|` in this way. This can be used inside groups as well. As the target string is scanned, REs separated by `|` are tried from left to right. When one pattern completely matches, that branch is accepted. This means that once A matches, B will not be tested further, even if it would produce a longer overall match. In other words, the `|` operator is never greedy. To match a literal `|`, use `\|`, or enclose it inside a character class, as in `[|]`.

`(...)`

Matches whatever regular expression is inside the parentheses, and indicates the start and end of a group; the contents of a group can be retrieved after a match has been performed, and can be matched later in the string with the \number special sequence, described below. To match the literals `(` or `)`, use `\(` or `\)`, or enclose them inside a character class: `[(]`, `[)]`.

`(?=...)`

Matches if `...` matches next, but doesn’t consume any of the string. This is called a lookahead assertion. For example, `Isaac (?=Asimov)` will match `Isaac ` only if it’s followed by `Asimov`.

`(?!...)`

Matches if `...` doesn’t match next. This is a negative lookahead assertion. For example, Isaac `(?!Asimov)` will match `Isaac ` only if it’s not followed by `Asimov`.

# Example

1. Check if the string is 24 hour time format

2. Validate whether the string
* Has one uppercase letters.
* Has two lowercase letters.
* Has two digits.
* Has one special case letter [!@#$&*].
* Is of length 8.
