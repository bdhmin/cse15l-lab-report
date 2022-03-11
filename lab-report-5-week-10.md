# Lab Report 4

**Bryan Min; A17153124**\
**March 11, 2022**

### Finding the files that don't match

I created a new method, `getLinks2()`, which is our parsing implementation and kept the `getLinks()` function the same. I then read the files in both ways, and checked if the two Arraylists were not equal. If they were not, I printed the file's filename and the contents of both results.


### CommonMark Spec Test 1

File: 498.md
```
[link](<foo(and(bar)>)
```

MarkdownParse Result:
`[]`

Our Implementation Result:
`[foo(and(bar)]`

We will parse strings inside `( )` since we only look for the next closing parentheses, so when the `[]()` is found through parse, it seems as though we do not consider the opening parentheses that are formed 

This will require some sort of way to keep track of all opening braces so those opening braces are not a part of a string that is supposed to be a part of the link.

### CommonMark Spec Test 2

File: 577.md
```
![foo](train.jpg)
```

MarkdownParse Result:
`[train.jpg]`

Our Implementation Result:
`[]`

The string in the md file is supposed to be an image, so we do not parse the string to a link. However, MarkdownParse falsely identifies the string as a link, missing the `!`.

This will require checking the index before finding `[`, but also making sure the index of `[` is not 0, since 0 - 1 = -1—this can result in an error.


