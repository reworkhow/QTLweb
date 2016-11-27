# regular expression with python

This post is not a thorough article about regular expression with python. Since I've been struggling with awk/sed for a long time, I haven't maneged to grasp these tools. The reason should be that it is really a bad idea to learn these kind of text processing tools through following a book instead of working with real problems. It is different from languages like C++ which require basic knowledge at first, and it's too boring for me. Today I saw something about regular expression in python and dicided to write down a shallow message about it. **The next time I pick it (text processing tools) up should be dealing with a real text-processing problem.** These are tools I can learn more easily and faster when dealing with a real problem.

Below is based on this [webpage](https://developers.google.com/edu/python/regular-expressions).



```
import re
text='Today it is Sunday! It is sunny but chilly! 36524!'
match=re.search(r'To',text)
if match:
    print 'found',match.group()
else:
    print 'not found'

> found To

```



> a, X, 9, 

```
ordinary characters just match themselves exactly.
```



> . (a period)



```
matches any single character except newline '\n'
```



> \b



```
boundary between word and non-word
```



> ^ = start, $ = end



```
match the start or end of the string
```



| symbol | meaning |
| :-- | :-- |
| \d | digit char |
| \w | word char |
| \t, \n, \r | tab, newline, return |
| \s | a single whitespace character including space, newline, return, tab, form [\n\r\t\f] |



```
match=re.search(r'..n',text)
if match:
    print 'found',match.group()
else:
    print 'not found'

>found Sun

match=re.search(r'\d\d\d',text)
if match:
    print 'found',match.group()
else:
    print 'not found'

>found 365

match=re.search(r'\w\w\w',text)
if match:
    print 'found',match.group()
else:
    print 'not found'  ##but just return the first one it found

>found Tod

```



> `+` --> 1 or more occurrences of the pattern to its left, e.g. 'i+' = one or more i's
> 
> `*` --> 0 or more occurrences of the pattern to its left
> 
> `?` --> match 0 or 1 occurrences of the pattern to its left

