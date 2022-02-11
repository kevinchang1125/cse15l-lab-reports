# **Week 6 Lab Report:** Streamlining SSH Configuration
>By Kevin Chang 2/11/2022
### In this lab report I will be going over how we can further increase ssh's efficiency through the config file!


# Editing the`.ssh/config` file
- The first step is to locate the .ssh folder on your device
- Since it starts with a '.' the folder is actually considered hidden and through your file explorer, you can update its Advanced Settings to show hidden folders

![Image](https://i.imgur.com/xy3cXYt.png)

- Within the .ssh, file we can create a file named 'config' if it does not already exist. (Mine had previously been created from past courses)
- We can open this by then dragging into a text editor of your choice, I used VS code

![Image](https://i.imgur.com/m3c9Mj0.png)

- There are now 3-4 lines that need to be added:
1) The first line (no indent) needs the keyword `Host` followed by the alias of your choice, I chose `ieng6` since that is the server I am attempting to login to. The host alias can have any name of your choosing
2) The second line (indented in) has the keyword `HostName` and the location we are attempting to login too which would be the ucsd ieng6 server so we would write `ieng6.ucsd.edu`
3) The third line (indented in) has the keyword `User` and followed by your username so for me, `cs15lwi22aju`
4) The fourth line (indented in) is optional if the first three lines do not work and would identify the key we have generated in the past. This differs between mac and windows but would either be `IdentityFile ~/.ssh/id_rsa_ucsd` or `IdentityFile ~/.ssh/id)ed25519` respectively
```
Host [alias]
    HostName [remote location]
    User [username]
    IdentityFile [file - depends on mac/windows]
```

![Image](https://i.imgur.com/6q7lv0X.png)

# Using our new `ssh` login
- After the config file is updated we can now simply login with:
```
ssh [alias]
```

![Image](https://i.imgur.com/9zaquYI.png)

- In our case our alias was `ieng6` so we simply typed in `ssh ieng6`

# `scp` with our new alias

- Now, our alias can replace most instances of typing our previous formula of
```
ssh [username] @ [remote location]

ssh [alias]
```
- We can try using the `scp` command with our new ssh config!

```
scp [file] [alias]

scp WhereAmI.java ieng6
```

![Image](https://i.imgur.com/ktsb3Xd.png)

- We can see we no longer need to type in the long combination of our username and remote location anymore!

>Thank you for reading!