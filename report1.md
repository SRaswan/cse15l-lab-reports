# Lab Report 1 - Remote Access and Filesystem
by Shaurya Raswan
<br>
## Installing VScode
Go to this [link](https://code.visualstudio.com/) and download and install VSCode for your system. Once you open VSCode, the screenshot should look like this:
![VSCode](/VSCode.png)
<br>
## Remotely Connecting
Now we can connect to the virtual servers for CSE 15L called ieng6. Open a file or create any file in VSCode (name it anything you want) and go to terminal on the bottom. Here we can type commands and remotley connect. For mac, you can just go to the app called 'Terminal'. If you have Windows, you can download git bash for VSCode specifically. No matter how you choose to connect remotley, type in ssh (secure shell) and your account to login to the ieng6 servers!
```
ssh cs15lwi23abc@ieng6.ucsd.edu
```
This uses your username for the class "cs15lwi23abc" but "abc" is specific to your account. After logging in, information will be printed to you like this:
![Connection](/connect.png)
<br>
Once you are logged in after typing your correct password and typing "yes" to allow a remote connection, we can try some commands. 
## Trying Some Commands
Here are a list of useful commands: <br>
```
cd ~ # Go home
cd # Change directory
ls -lat # Looks at all folders in the directory with permissions and other cool info
ls # Looks at all folders in the directory
cp hello.txt /location/ # Copies hello.txt into folder location
cat hello.txt # Reads the file
touch hello.txt # Makes file
vi hello.txt # Use VIM to edit a file
```

Try out these commands for manuvering to different directories, making files, reading files, copying files, and so on. What if you want to create and edit a file? We can use vim to edit a file. Use the `touch` command to make a file, type `vi` to edit that file. Now we are in a text editor. Type `i` to be in INSERT mode. Now we can type whatever we want, like "Hello World!!!". To save and exit, type `:wq`. Now, our terminal should look something like this:
![HelloWorld](/helloworld.png)

Using `cat` to read the file allows us to actually see our edits to `hello.txt`. Good job! We are done!
