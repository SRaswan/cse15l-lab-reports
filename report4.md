# Lab Report 4 - The Competition
by Shaurya Raswan

## 4. Log into ieng6
First, we log into ieng6. Assuming we do not already have it in our history, the terminal should look something like this.
<img width="718" alt="Screen Shot 2023-02-26 at 11 45 12 PM" src="https://user-images.githubusercontent.com/42948407/221503825-00fcea22-3c9f-47d8-9479-dae5cb08a52c.png">\
Typed: `ssh cs15lwi23aks@ieng6.ucsd.edu<enter>` <br>
The ssh command means we are attemping to secure connect to a server that we have access to (our remote account on UCSD's ieng server). <br>
Assuming we do not have SSH Keys for ieng6, we then type our password and then `<enter>`. However, we can skip this step if we generate SSH keys for ieng6. To do this, follow these steps. In your local terminal, run `ssh-keygen`. Keep entering `<enter>` until the program shows some text it calls the “randomart image”. Log into your account on ieng6 like before. Run `mkdir .ssh` in the terminal. Logout of the remote account. Copy the public SSH key you created onto your remote account, specifically inside the `.ssh` directory you just created, in a file called `authorized_keys`. Scroll up a bit to where you were creating the SSH key, find the line where it says: `Your public key has been saved in: <path to your public SSH key>`, copy the path. Make sure you get the public key file, ending in `.pub`, here, not the private file. From your local computer, run `scp <path to your public SSH key> cs15lwi23__@ieng6.ucsd.edu:~/.ssh/authorized_keys`. Enter password when prompted (this will be the last time). Log onto your remote account again, you shouldn’t be prompted for a password anymore.
 
## 5. Clone your fork of the repository from your Github account
<img width="529" alt="Screen Shot 2023-02-27 at 12 00 18 AM" src="https://user-images.githubusercontent.com/42948407/221506629-631562ff-561a-46d1-b3d2-80ca04b2306e.png">\
Typed: `git clone git@github.com:SRaswan/lab7.git<enter>` <br>
Using the git clone command, we can clone using the SSH key. This creates the lab7 repository in our directory from our GitHub fork. We can do this because our account is verified with the public SSH key authenticated on our GitHub account. This allows us to easily clone, commit, add, and push. We can also use git SSH keys for GitHub authorization directly saved on the server. Similar to generating the SSH key for our password above, we can do something similar but instead generate SSH keys directly on the remote desktop and put it in our GitHub settings.

## 6. Run the tests, demonstrating that they fail
<img width="709" alt="Screen Shot 2023-02-27 at 12 03 10 AM" src="https://user-images.githubusercontent.com/42948407/221507191-65e6187a-4abd-4115-b5c4-d2dc8162d2da.png">\
Typed: `cd lab7<enter>`, `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java<enter>`, `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples<enter>` <br>
We first traverse to lab7 directory. Then we compile all the java files, ListExamples.java and TestListExamples.java. Then we run our test file that tests ListExamples.java with JUnit. 2 tests are run and 1 fails.

## 7. Edit the code file to fix the failing test
<img width="415" alt="Screen Shot 2023-02-27 at 12 15 20 AM" src="https://user-images.githubusercontent.com/42948407/221509770-65a20009-0375-45a3-b36e-19ac21b4861d.png">
<img width="707" alt="Screen Shot 2023-02-27 at 12 14 59 AM" src="https://user-images.githubusercontent.com/42948407/221509789-48494301-0e04-4d02-82bb-63fe2c08b519.png">
<img width="709" alt="Screen Shot 2023-02-27 at 12 12 37 AM" src="https://user-images.githubusercontent.com/42948407/221509805-125c254e-a98a-4f1b-ba62-b0c362a79939.png">\
Typed: `nano ListExamples.java<enter>`, `<^W>(index2 <`, `<down><down><right><right><right><backspace>2`, `<^X>Y<enter>` <br>
First, we use the nano command to change the contents of the file. To fix the error, all we need to do is fix the last while loop where index1 is incremented by accident instead of index2. To get there the fastest without constantly doing `<down>`, we can using `<^W>` to search the file for `(index2 <`. This puts our cursor at the start of the while loop. Then we press `<down>` twice and `<right>` three times. Then we delete the `1` and make it `2`. To exit, we do `<^X>`, where then we are prompted to save the buffer by pressing `Y` for yes. We say yes and press enter to save the changes and exit. Now, we have our file fixed.

## 8. Run the tests, demonstrating that they now succeed
<img width="709" alt="Screen Shot 2023-02-27 at 12 24 56 AM" src="https://user-images.githubusercontent.com/42948407/221511578-3f6e9e19-8c26-448d-85bf-5df492aabd50.png">\
Typed: `<up><up><up><enter>`, `<up><up><up><enter>` <br>
The `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` command was 3 up in the search history, so I used up arrows 3 times. Then the `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore` command was also now 3 up in the history. Now it shows 2 sucesses and no failures with JUnit.

## 9. Commit and push the resulting change to your Github account (you can pick any commit message!)
<img width="709" alt="Screen Shot 2023-02-27 at 12 26 27 AM" src="https://user-images.githubusercontent.com/42948407/221511912-8a7b6351-1114-492c-8919-1e5cdb43bc56.png">
<img width="707" alt="Screen Shot 2023-02-27 at 12 26 08 AM" src="https://user-images.githubusercontent.com/42948407/221511955-bd101aca-29f3-46d5-b324-e3bde2b648a7.png">
Typed: `git add *<enter>`, `git commit<enter>`, `<i>done`, `<escape>:wq<enter>`, `git push<enter>` <br>
First we git add all the files that we changed or added. Then we commit with the `git commit` command. This prompts us to write a commit message in vim. Type `i` to be in INSERT mode, which it will show on the bottom. Now we can type whatever we want directly on the file for our commit message. To save and quit, type `:wq` in COMMAND mode (press `esc` key to enter COMMAND mode anytime). When we enter, we can now `git push` because we are in our terminal. This pushes all the new changes to our GitHub repository!

