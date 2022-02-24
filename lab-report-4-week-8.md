# Lab Report 4

**Bryan Min; A17153124**\
**February 25, 2022**

[Link to Reviewed Repo](https://github.com/iireneliao/markdown-parse)

[Link to my MarkdownParse Repo](https://github.com/bdhmin/markdown-parse)

Reviewed code JUnit test case fails, and this is the result:

### Snippet 1

The JUnit test I ran

```
@Test
public void test1() throws IOException {
    Path file = Path.of("snippet-1.md");
    String contents = Files.readString(file);

    assertEquals(List.of("`google.com", "google.com", "ucsd.edu"), MarkdownParse.getLinks(contents));
}
```

#### Snippet 1 - Reviewed (failed)

```
1) test1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.test1(MarkdownParseTest.java:50)
```

#### Snippet 1 - Mine (failed)


```
1) test1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.test1(MarkdownParseTest.java:53)
```



### Snippet 2

The JUnit test I ran

```
@Test
public void test2() throws IOException {
    Path file = Path.of("snippet-2.md");
    String contents = Files.readString(file);

    assertEquals(List.of("a.com", "a.com(())", "example.com"), MarkdownParse.getLinks(contents));
}
```

#### Snippet 2 - Reviewed (failed)

```
2) test2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[a.com, a.com((]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.test2(MarkdownParseTest.java:58)
```

#### Snippet 2 - Mine (failed)

```
2) test2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[a.com, a.com((]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.test2(MarkdownParseTest.java:61)
```

### Snippet 3

The JUnit test I ran

```
@Test
public void test3() throws IOException {
    Path file = Path.of("snippet-3.md");
    String contents = Files.readString(file);

    assertEquals(List.of("https://ucsd-cse15l-w22.github.io/"), MarkdownParse.getLinks(contents));
}
```

#### Snippet 3 - Reviewed (failed)

```
3) test3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://ucsd-cse15l-w22.github.io/]> but was:<[
    https://www.twitter.com
, 
    https://ucsd-cse15l-w22.github.io/
, github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.test3(MarkdownParseTest.java:66)
```

#### Snippet 3 - Mine (failed)


```
3) test3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://ucsd-cse15l-w22.github.io/]> but was:<[
    https://www.twitter.com
, 
    https://ucsd-cse15l-w22.github.io/
, github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.test3(MarkdownParseTest.java:69)
```

### Questions

1. Do you think there is a small (<10 lines) code change that will make your program work for snippet 1 and all related cases that use inline code with backticks? If yes, describe the code change. If not, describe why it would be a more involved change.

I believe a solution to this problem seems to be to not parse at all when a backtick character is found. Until the backtick is closed, we do not parse any characters inside, regardless of whether the characters inside the backticks contain brackets or parentheses. After the backtick, we continue to parse, saving the indices that we may have stored before the backticks were found. If we find that the text is link-parsable we return the link with the backtick text inside; if not, we do not return the link.

2. Do you think there is a small (<10 lines) code change that will make your program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets? If yes, describe the code change. If not, describe why it would be a more involved change.

I see this solution as potentially simple. The bracket search can be run recursively until the bracket search fails. This recursive function can return a boolean on whether a link has been parsed, and this will let the higher level in the stack to know that the upper layer link can be further parsed. This way the inner-most nested link will be parsed if it is parsable and nothing inside of it will be, and the outer link will be parsed if the inner string is not parsable.

3. Do you think there is a small (<10 lines) code change that will make your program work for snippet 3 and all related cases that have newlines in brackets and parentheses? If yes, describe the code change. If not, describe why it would be a more involved change.

I believe this fix is simple because it seems as though if one newline character is present the parsing continues but if there are more than one recurring newline character, then we do not parse the link. This will be an index check to see for if a newline character is found, if the next character is also a newline character. Depending on this result, we will either continue to parse the link or stop.
