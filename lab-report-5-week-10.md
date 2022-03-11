# **Week 10 Lab Report:** Differences between MarkdownParses
>By Kevin Chang 3/11/2022

### In this lab we will examine two specific commonmark-spec tests where our implementation of MarkdownParse differed from the MarkdownParse we used in the week 9 Lab.

# Differences

### To find these differences I ran both of the bash scripts, redirected the output into their own files, and compared the two results side by side by scrolling simultaneously. I could have also used the `diff` method call but it was fun scrolling down and seeing the differences manually.

## Commands run: 
- The bash script is included here
```
for file in test-files/*.md;
do
  echo $file
  java MarkdownParse $file
done
```
- `bash script.sh > results9.txt`
- runs the script and redirects the output to a text file for the week 9
- The format (from the bash file) prints the file number on one line and the output on another line

![image](https://i.imgur.com/GNdKtOB.png)

![image](https://i.imgur.com/zYM3msF.png)
 
 - we run the same command for our own MarkdownParse implementation and redirect the output to a file named `myresults.txt`
 - Note my *terrible* spelling of `sciprts.sh` which I was too lazy to change after I made the bash file :(

## Looking at the Output
![image](https://i.imgur.com/JTMaPZb.png)

- For this first image, we can see the differences on **Line 269** which corresponds to test file number 22 or `test-files/22.md`
- In this image, our MarkdownParse version has an output while the week 9 version has no output

![image](https://i.imgur.com/fgE2xgO.png)

- For this first image, we can see the differences on **Line 936** which corresponds to test file number 519 or `test-files/519.md`
- In this image, the week 9 version has an output while our MarkdownParse version has no output

# Difference 1: Test File 22
![image](https://i.imgur.com/2komJD8.png)

![image](https://i.imgur.com/HOkwXUA.png)

- Here, we can see the test file contents and its expected output on the commonmark demo website
- We can scroll back up and see that our Markdownparse version has an output which differs from the week 9 output of no links.
- Our version prints out the contents of the parenthesis and recognizes it as a link which is incorrect 
- The string inside the parenthesis is not a valid link and therefore no links should be retrieved

![image](https://i.imgur.com/sk4bFoy.png)
- If we look at our code, we have nothing to check if the contents of the parenthesis are a valid link or not so as long as we have the brackets and parenthesis structure, the contents inside the parenthesis would be considered a link
- For this test, a quick fix would be checking if the contents of the parenthesis contain a `.` since all URLs contain a period
- Adding that quick check would fail that link's contents and should fix the bug accordingly to print an empty output


# Difference 2: Test File 519
![image](https://i.imgur.com/lSyNvYh.png)

![image](https://i.imgur.com/7L3xAj1.png)

- Here, we can see the test file contents and its expected output on the commonmark demo website
- We can scroll back up and see that the week 9 MarkdownParse version has an output which differs from our version which has no output
- This test file is actually an image (exclamation mark before the square brackets) and therefore no links should be retrieved 

![image](https://i.imgur.com/BzWGLpo.png)
- Looking at the week 9 MarkdownParse, we can see that there are no checks for exclamation marks anywhere in the `getLinks` method
- This means any image would be included within a call to `getLinks`
- This can quickly be fixed as seen in *our* implementation of MarkdownParse where we check if the character before the first square bracket is an exclamation mark, and we would skip that link if an exclamation mark is found
- That quick check would correctly have the week 9 markdown parse recognize any images it may come across and have it print an empty output in this case

>Thank you for reading!