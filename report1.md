# Lab Report 1 - Remote Access and Filesystem
by Shaurya Raswan
<br>
## Installing VScode
Go to this [link](https://code.visualstudio.com/) and download and install VSCode for your system. Once you open VSCode, the screenshot should look like this:
![VSCode](/VSCode.png)

## Remotely Connecting
Now we can connect to the virtual servers for CSE 15L called ieng6. Open a file or create any file in VSCode (name it anything you want) and go to terminal on the bottom. Here we can type commands and remotely connect. For mac, you can just go to the app called 'Terminal'. If you have Windows, you can download git bash for VSCode specifically. No matter how you choose to connect remotely, type in ssh (secure shell) and your account to login to the ieng6 servers!
```
ssh cs15lwi23abc@ieng6.ucsd.edu
```
This uses your username for the class "cs15lwi23abc" but "abc" is specific to your account. After logging in, information will be printed to you like this:
![Connection](/connect.png)

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
rm hello.txt # Removes file
vi hello.txt # Use VIM to edit a file
```

Try out these commands for maneuvering to different directories, making files, reading files, copying files, and so on.
<img width="652" alt="Commands" src="https://user-images.githubusercontent.com/42948407/215295339-5065e041-c652-4f43-9ced-19e06b89144f.png">
This is what the terminal should look like when you login. When we type `ls -lat` above, it shows us all the files in the current directory (even the hidden ones). We see that he have a hello.txt file in the folder. Lets type `cat hello.txt` to read it. We also have a directory called perl5, so lets copy hello.txt in perl5 by doing `cp hello.txt /perl5/`. Nothing showed up when we copied the file, which is okay! The terminal often does not tell us if we suceeded if we did, it just shows nothing. Lets type `cd perl5` to move to that directory and see if hello.txt is there with `ls`. Not lets read hello.txt again to see if all content was copied, too.
<img width="412" alt="Copy file" src="https://user-images.githubusercontent.com/42948407/215295722-9a62cab2-35b4-48b6-9b27-58fb6878063a.png">
Nice!

## Trying out VIM
What if you want to create and edit a file? If you do not have that hello.txt text file that I had, then we can use vim to edit a file. Use the `touch` command to make a file, type `vi` to edit that file. 
<img width="814" alt="VIM" src="https://user-images.githubusercontent.com/42948407/215295453-073cebc5-e8d2-44d3-b302-f8c930256e79.png">
When you are in the text editor, it should look like how it does above. VIM has 2 modes, intert mode and command mode. Command mode is what we are in right now, and it lets us do certain commands without directly typing on the file (like saving, deleting an entire line where your cursor is with `dd`, pasting an entire line by copying where your cursor is with `yy` and then pasting with `pp`, and so on). Type `i` to be in INSERT mode, which it will show on the bottom. Now we can type whatever we want directly on the file, like "Hello World!!!". To save and quit, type `:wq` in COMMAND mode (press esc key to enter COMMAND mode anytime). Now, our terminal should look something like this when we quit and saved:
![HelloWorld](/helloworld.png)

Using `cat` to read the file allows us to actually see the content of our file `hello.txt` now. Good job! We are done!
