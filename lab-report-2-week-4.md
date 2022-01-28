# **Week 4 Lab Report:** Fixing Accumulating Tests
>By Kevin Chang 1/27/2022

# Bug 1: Not Parsing Parenthesis Correctly
![Image](https://i.imgur.com/do6DlHE.png)

### [Link to breaking file for Bug 1](https://github.com/kevinchang1125/markdown-parse/blob/main/break.md)

### Output:
```
[https://something.com, some-page.html, is cool, some-page.html]
```
- As we can see from the output, the symptom is that the links are incorrectly parsed if there are spaces or additional text in between the square brackets and the parenthesis
- The bug is that the original MarkdownParse file had no checking condition to see if the parenthesis immediately followed the square brackets--this led to our output containing `is cool` which is merely some text within parenthesis after an instance of square brackets a few lines above it
- We fixed the bug by adding a checking condition for parenthesis immediately following square brackets to verify this is a link and not an instance of square brackets and parenthesis separated

# Bug 2: Displaying Images (It shouldn't!)
![Image](https://i.imgur.com/t4Uuymh.png)

### [Link to breaking file for Bug 2](https://github.com/Cubified/markdown-parse/blob/main/test-file6.md)

### Output:
```
[page.com]
```
- The symptom is that image links are not treated differently from website links and are still output even though we only want to output website links
- This led to the failure inducing input, `![link](page.com)`, still being recognized as a link, and therefore MarkdownParse still output `page.com` even though it was an image link.
- The bug is that the original Markdownparse file had no checking condition to see if there was an exclamation mark before the square brackets, meaning the link was actually an image--we fixed this by adding checking conditions that the character before the square bracket was an exclamation mark or by checking if the first character was an exclamation mark followed by square brackets as the first method would cause an out of bounds error if the exclamation mark was the first character in a line


# Bug 3: No Closed Paranthesis...
![Image](https://i.imgur.com/ORJfWCG.png)

### [Link to breaking file for Bug 3](https://github.com/Cubified/markdown-parse/blob/main/breaking_test_3.md)

### Output:
```
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: begin 4, end -1, length 6
```
- The failure inducing input does not contain the last closed parenthesis which would normally end a link
- The bug is that the MarkdownParse assumes there will always be another closed parenthesis--we fix this by checking for all the brackets and parenthesis at the beginning of the file and updating our methods accordingly in case some or all are missing
- The symptom is that if the read file has no closing parenthesis, the output as seen above, can result in an IndexOutOfBoundsException 


>Thank you for reading!