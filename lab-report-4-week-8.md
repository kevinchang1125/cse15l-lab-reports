# **Week 8 Lab Report:** Additional MarkdownParse Tests
>By Kevin Chang 2/25/2022

## 1. Respositories Used:
### Thursday 10 AM [Patoo](https://github.com/kevinchang1125/markdown-parse) (Mine)

### Thursday 10 AM [Bull Mastiff](https://github.com/IncogOwl/markdown-parse) (Reviewed)

## 2. Valid links and what we expect for each test:

### Snippet 1
![Image](https://i.imgur.com/H3M9Mnr.png)

We expect as valid links:
```
 [`google.com, google.com, ucsd.edu]
```

### Snippet 2
![Image](https://i.imgur.com/11qfMqj.png)

We expect as valid links:
```
 [a.com, a.com(()), example.com]
```

### Snippet 3
![Image](https://i.imgur.com/ixb5oaA.png)

We expect as valid links:
```
 [https://ucsd-cse15l-w22.github.io/]
```

# JUnit tests for the 3 code snippets
![Image](https://i.imgur.com/RC34n34.png)

- To make the JUnit tests, we first made a standard test method and added the `throws IOException`
- The next 2 lines let MarkdownParse read the markdown files we are testing, so finding the path of `snip1, snip2, snip3` and reading their contents as the arg for MarkdownParse
- The last 2 lines just test to see if their outputs were equivlant--We check our expected value against our actual results from our/their MarkdownParse file

# Our implementation
## **All Tests Failed**
![Image](https://i.imgur.com/EjrmoAP.png)


# Implementation we reviewed 
## **All Tests Failed**
![Image](https://i.imgur.com/0hM2JR9.png)

# Snippet 1 MarkdownParse changes
- To address backticks, I believe we would have to count their current position similar to how we track the positions of brackets and parentheses. 
- I think this would be a more involved case and would take **more** than 10 lines since there are a multitude of cases such as just one backtick, backticks in the brackets, backticks in the parenthesis, and any combination where backticks are in and out of the two. 
- While there would be some overlap when checking for all these cases, I still think this would take several if statements and would be over 10 lines.

# Snippet 2 MarkdownParse changes
- I think we can address this issue briefly since the only issue we would have to address would be the nested parentheses and brackets as the other issues we catch.
- To make this fix, we would have to count the number of open parentheses (after brackets) and see if the number of closed parentheses match before taking the valid link within the outermost parentheses.

# Snippet 3 MarkdownParse changes
- I think this would also be a quick fix since we can just also search for `\n` when also parsing for brackets and parentheses.
- Once we locate the `\n`, we can simply just skip those 2 characters and continue parsing for links and searching for another newline sequence if there are more in the file.



>Thank you for reading!