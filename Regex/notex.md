```
.  - matches everytching
```

```
\.  - match evry dot ("\" is an escape charater)
```

```
\\ \ - search for back slash
```

```
.       - Any Character Except New Line
\d      - Digit (0-9)
\D      - Not a Digit (0-9)
\w      - Word Character (a-z, A-Z, 0-9, _)
\W      - Not a Word Character
\s      - Whitespace (space, tab, newline)
\S      - Not Whitespace (space, tab, newline)

\b      - Word Boundary
\B      - Not a Word Boundary
^       - Beginning of a String
$       - End of a String

[]      - Matches Characters in brackets
[^ ]    - Matches Characters NOT in brackets
|       - Either Or
( )     - Group

Quantifiers:
*       - 0 or More
+       - 1 or More
?       - 0 or One
{3}     - Exact Number
{3,4}   - Range of Numbers (Minimum, Maximum)


#### Sample Regexs ####

[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+
```



examples:

```
\d\d\d[-.]\d\d\d[-.]\d\d\d  - eg. match phone number with separator "-"
```

```
[1-9] any number between 1 and 9
```

```
[a-zA-z] - matches any letter small and capital
```

```
[^b]at - anything that is not "b" and follow "at"
```

```
\d{3}.\d{3}.\d{4}  - matches 3 digits thant any 3 digits any and 4 digits 
```

```
@.?o[a-z]\w*  - matches zero or norne character after "@" than letter "o" that any small letter than any word zero or more
```

