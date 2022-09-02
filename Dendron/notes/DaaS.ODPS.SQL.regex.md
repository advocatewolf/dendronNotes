---
id: td8ofxehc793wc883a67koq
title: Regex
desc: ''
updated: 1661507457669
created: 1661506970472
---
[ref.](https://www.alibabacloud.com/help/en/maxcompute/latest/regular-expressions)

Metacharacter  | Description
---------------|------------
^  | Matches the beginning of a string.
$  | Matches the end of a string.
.  | Matches any single character.
*  | Matches zero or more instances of the preceding character or character pattern.
+  | Matches one or more instances of the preceding character or character pattern.
?  | Matches zero or one instance of the preceding character or character pattern.
?  | Matches a modifier. If this character follows one of other characters (*, +, ?, {n}, {n,}, or {n,m}), the match pattern is non-greedy. In the non-greedy algorithm, a character string matches as few characters as possible. In the greedy algorithm, a character string matches as many characters as possible. By default, the greedy algorithm is used.
A\|B  | Matches A or B.
(abc)*  | Matches zero or more instances of the abc sequence.
{n} or {m,n}  | The number of matches.
[ab]  | Matches any character in the brackets. The character can be a or b. Fuzzy match is used.
[a-d]  | Matches one of the following characters: a, b, c, and d.
[^ab]  | Matches any character except those in the square brackets.
[::]  | For more information, see the following table.
\  | The escape character.
\n  | n is a digit from 1 to 9 and is backward referenced.
\d  | Digits.
\D  | Non-digit characters. 