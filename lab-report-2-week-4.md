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


# Bug 3: 
![Image]()

Pick three code changes that your group worked on in labs 3 and 4 in order to fix a bug; these should be stored as commits on someone’s repository. Fork the repository so you have your own copy with all the work your group did if you haven’t already.

For each of the three code changes:

Show a screenshot of the code change diff from Github (a page like this)

Link to the test file for a failure-inducing input that prompted you to make that change

Show the symptom of that failure-inducing input by showing the output of running the file at the command line for the version where it was failing (this should also be in the commit message history)

Write 2-3 sentences describing the relationship between the bug, the symptom, and the failure-inducing input.