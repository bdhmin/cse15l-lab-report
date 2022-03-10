# Lab Report 4

**Bryan Min; A17153124**\
**March 11, 2022**

### Finding the files that don't match

I created a new method, `getLinks2()`, which is the CommonMark parsing implementation and kept the `getLinks()` function the same. I then read the files in both ways, and checked if the two Arraylists were not equal. If they were not, I printed the file's filename and the contents of both results.


### CommonMark Spec Test 1

File: 498.md
```
[link](<foo(and(bar)>)
```

MarkdownParse Result:
`[]`

CommonMark Result:
`[foo(and(bar)]`

CommonMark will parse strings inside `< >` as links, so when the `[]()` is found through parse, it seems as though CommonMark is omitting `< >`. 

It appears that CommonMark as different rules when parsing links, as it considers other ways to create links. This would probably take removing the rule to consider the `< >`, which will be a lot of code.

### CommonMark Spec Test 2

File: 577.md
```
![foo](train.jpg)
```

MarkdownParse Result:
`[train.jpg]`

CommonMark Result:
`[]`

The string in the md file is supposed to be an image, so CommonMark does not parse the string to a link. However, MarkdownParse falsely identifies the string as a link, missing the `!`.

This will require checking the index before finding `[`, but also making sure the index of `[` is not 0, since 0 - 1 = -1—this can result in an error.


