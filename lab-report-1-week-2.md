# **Week 2 Lab Report:** Logging into `ieng6` remotely
>By Kevin Chang 1/13/2022

## 1. Installing VScode
- VS code is a popular text editor we will use to remotely connect to a remote server and copy over our files
- Search up "VS code" in any browser and download it with your device's respective specifications (Mac, Windows, Linux, etc.)
![Image](https://i.imgur.com/G8g03vZ.png)


## 2. Remotely Connecting
- Open VS code and you should be greeted with a welcome page
- At the very top of the screen, you can click terminal, and select new terminal
- You can also hit ``` ctrl + shift + ` ``` to open a new terminal
![Image](https://i.imgur.com/iFqPvy9.png)
- At this point, you should know your ieng6 account's username and password, but if you do not, you can look up this information/reset your password here: [Username and password lookup](https://sdacs.ucsd.edu/~icc/index.php)

- From here, you can remotely connect by typing in the command: 
```
ssh cs15lwi22aju@ieng6.ucsd.edu
```
- It will then ask for your password which you can type in (It will not show any input but it is recorded still)
- A successful login will display below
![Image](https://i.imgur.com/M9HFEvx.png)


## 3. Trying some commands
- Now that we are logged in, there are various commands we can try in the remote server! 
- Note: There are many more but this table displays a few notable commands

| Command | What it does |
|---------|--------------|
|```ls``` |Displays all files currently in your directory|
|```ls -a``` |Displays all files currently in your directy *including* hidden files   
|```cd [directory]``` |Moves to the directory listed after the command|
|```cd ..``` |Moves to the directory above your current directory|
|```cd ~``` |Returns to your home directory|
|```mkdir [name]``` |Creates a directory with name given              |
|```cat``` |Displays a file's contents to the terminal|
|```cp [file] [destination]``` |Copies a file to the destination listed|
|```exit``` |Exits the remote session|

- Example of some commands being run

![Image](https://i.imgur.com/PJJDM93.png)


## 4. Moving files with `scp`
- We can move files from our client to the server using the `scp` command
- Make sure you are not logged in to `ssh` for this step!
- Also check you are in the same directory as the file you want to move over on the client side
- Use the command and it will request your password again:
```
scp [File name] cs15lwi22aju@ieng6.ucsd.edu:~/
```
![Image](https://i.imgur.com/P6Sa38l.png)
- As we can see, the file "WhereAmI.java" has been moved over onto my ieng6 account and can be run remotely!


## 5. Setting an SSH Key
- We can set an `ssh` key to log in to our ieng6 account without having to type in our password
- If you are on Windows, see more steps [here](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement#user-key-generation)
- Run the command which will create a set of keys:
```
ssh-keygen
```
- The keys are public and private-- we want to copy the public key to the server and keep the private key on the client side. After, `ssh` can use the pair of keys instead of typing in your password
- We need to create a place to store the public key on the server:
```
mkdir .ssh
```
- Now we want to log out and move the files to the ".ssh" directory using `scp`
```
scp [file path of public key in your computer] cs15lwi22aju@ieng6.ucsd.edu:~/.ssh/authorized_keys
```
- After, you should be able to log in without a password
![Image](https://i.imgur.com/La2mWkr.png)


## 6. Optimizing Remote Runing
- We can optimize remote running even further through the use of quotations and semicolons
- Using quotes after a `ssh`, we can immediately run the command in quotations on the ieng6 server and exit!
```
ssh cs15lwi22aju@ieng6.ucsd.edu "ls"
```
- We can separate multiple commands on the same line with semicolons
```
javac WhereAmi.java; java WhereAmI
```
- We can see a demonstration of both below--The two commands of "javac" and "java" are first separated with a semicolon meaning they will run consecutively. Next, both commands are surrounded by quotations meaning they will run once on the server before exiting automatically! 
![Image](https://i.imgur.com/fT3ebVS.png)

- If we were to run each command individually and without our automatic login: 
    - Login to ssh (one line) `ssh cs15lwi22aju@ieng6.ucsd.edu`
    - Type in our password (one line)
    - Compile our file (one line) `javac WhereAmI.java`
    - Run our file (one line) `java WhereAmI`
- If we were to have each line ready, and counted copy paste "ctrl+c and ctr+v" as two keystrokes, and hitting enter as another keystroke, this would total 12 keystrokes!
- Through what we learned however, we can combine all of the steps into one line as show in the image! If we just have the line below and copy paste it and hit enter, our total would only be 3 keystrokes:
```
ssh cs15lwi22aju@ieng6.ucsd.edu "javac WhereAmI.java; java WhereAmI
```
- This saved me 11 seconds (with our improved version totaling at around just 2 seconds)!

>Thank you for reading! 

