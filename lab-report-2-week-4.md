# Lab Report 2

**Bryan Min; A17153124**\
**January, 26, 2022**

### Code Change 1 - Check for incorrect brace indices

In [Lines 17 to 19](https://github.com/bdhmin/markdown-parse/commit/d66a8a1875fc47fa224c34eb7569cf44ae029df2), if any brace index is invalid, then we exit out of the parse loop.

<img width="889" alt="Screen Shot 2022-01-28 at 11 46 27 AM" src="https://user-images.githubusercontent.com/43192371/151611701-f70f3328-4e85-4c22-a88b-0b19da11fc9c.png">

We found this error when there was additional text that came after a found link using this [test file](https://github.com/bdhmin/markdown-parse/blob/main/break-file-1.md).

The symptom of this error was an infinite loop:\
<img width="311" alt="Screen Shot 2022-01-28 at 11 31 39 AM" src="https://user-images.githubusercontent.com/43192371/151609837-2b67bde8-2518-4783-821c-d73b0206fc75.png">

The bug did not account for the possible return values of the method `.indexOf()` to return `-1` and thus the symptom of infintely looping resulted. The current index would always be set to `-1 + 1 = 0` since the indices could not be found, and so the while loop could not progress. Our input had more text afterwards that were not links but because there was no exit case for not finding a link, the program assumed a link was still in the file.

### Code Change 2 - Check for correct link parsing

In [Lines 20 to 22](https://github.com/bdhmin/markdown-parse/commit/d66a8a1875fc47fa224c34eb7569cf44ae029df2), if the `]` is not immediately followed by `(`, the string is not considered a link.

<img width="630" alt="Screen Shot 2022-01-28 at 11 44 56 AM" src="https://user-images.githubusercontent.com/43192371/151611515-d2952401-fb70-4553-b520-6aa4ec8c4577.png">

We found this bug when we attempted to create a link that contained text in between the text portion and the link portion of the link string using this [test file](https://github.com/bdhmin/markdown-parse/blob/main/break-file-2.md).

The symptom of this error was a false positive—the string was considered to be a link when it should not have:\
<img width="320" alt="Screen Shot 2022-01-28 at 11 50 43 AM" src="https://user-images.githubusercontent.com/43192371/151612201-e664d7c1-8c2a-49fb-9411-176922313a43.png">

The input file was made so that a the link parse would be challenged if the braces existed in the correct order, but not glued together like `[<text>](<link>)`. Because the code did not account for the text in between, the symptom was false positive and incorrectly parsed the inputted link.

### Code Change 3 - Both text and link must contain text
