# Lab Report 3
by Shaurya Raswan

## The `grep` Command
Lets say we have the skill-demo1-data repository on our local computer. We can retrive it by doing `git clone https://github.com/ucsd-cse15l-w23/skill-demo1-data`. Here we can use the grep command to search and match through directories and files in the skill-demo1-data repo.

## The `-r` option
The `-r` option stands for recursive. This means that the command recursivley goes through each file in the repository looking for the string that maches the one listed string, or "pattern". For example, we can use the grep option like this in the skill-demo1-data repository on the home directory (in the skill-demo1-data folder).<br>
Input:
```
grep -r 'Ringsend'
```
Output:
```
written_2/travel_guides/berlitz1/WhatToDublin.txt:        the RDS. Greyhound racing is on at Shelbourne Park, Ringsend, and at
written_2/travel_guides/berlitz1/WhereToDublin.txt:        Grand Canal Basin, Ringsend, off Pearse Street, Dublin
```
The command recursivley looks for all content in each file in all of the folders, starting from the current directory path. It looks for the word "Ringsend" througout all the content and outputs the file paths and part of the content that contains the word in context. This is extremley helpful because otherwise we would need to state a single filepath in the grep command like `grep 'Ringsend' file/path'`. The recursive option lets us look at multiple files instead of just one. Another example shows if we use two words. <br>
Input:
```
grep -r 'rive droite'
```
Output:
```
written_2/travel_guides/berlitz2/Paris-WhereToGo.txt:The sprawling Right Bank (rive droite) covers the whole range of Paris’s social life, from ultra-chic to downright sleazy. It claims the most luxurious shopping areas, the presidential Elysée Palace, the grands boulevards and financial district, but also, farther north, seamy Clichy and Pigalle, as well as hilly Montmartre, where modern art could be said to have begun. Back in the middle of it all, the huge Louvre museum makes its own magnificent statement. Just to the east, Les Halles, Beaubourg (around the Centre Georges-Pompidou), and place de la Bastille have each been transformed by controversial projects. The variety and energy of the nightlife here has overtaken that of the Left Bank. Even the charming old Marais and its Jewish quarter, representing the old Paris of the 17th century, have taken on a new fashionable appearance with the influx of trendy boutiques.
```
Here we can see that we can recursivley look for two words right next to eachother. In this way we can search for entire phrases or sentences. <br>
Source: https://www.gnu.org/software/grep/manual/grep.html

## The `-l` option
The `-l` option suppresses the normal output by only printing the file name, not the context for which the word is in. Therefore, it does not show the content of any files.<br>
Input:
```
grep 'tower' ./written_2/travel_guides/berlitz2/Paris-WhereToGo.txt -l
```
Output:
```
./written_2/travel_guides/berlitz2/Paris-WhereToGo.txt
```
Here the option is not very helpful because we already know the file that we are using grep on (as we had to type it out in the first place). However, the output does not show where 'tower' is used, which makes the output much less cluttered than it would be without `-l`. In fact, tower is shown 16 times. The commands above in the `-r` section show very cluttered outputs. Only showing filenames expecially helpful when we recursivley go through mutliple files. We can pair this option with the `-r` option.<br>
Input:
```
grep -r 'Dublin' -l
```
Output:
```
.git/index
written_2/non-fiction/OUP/Kauffman/ch1.txt
written_2/travel_guides/berlitz1/HistoryDublin.txt
written_2/travel_guides/berlitz1/IntroDublin.txt
written_2/travel_guides/berlitz1/IntroFrance.txt
written_2/travel_guides/berlitz1/WhatToDublin.txt
written_2/travel_guides/berlitz1/WhatToIbiza.txt
written_2/travel_guides/berlitz1/WhereToDublin.txt
```
Here every file is checked recursivley for 'Dublin'. Instead of printing out all the content for each file, it only shows file names. This is many files, so it would look much more convoluted without the `-l` option. <br>
Source: https://man7.org/linux/man-pages/man1/grep.1.html

## Sources
`man grep` shows helpful options and a description of grep.
https://www.gnu.org/software/grep/manual/grep.html
https://man7.org/linux/man-pages/man1/grep.1.html
https://www.geeksforgeeks.org/grep-command-in-unixlinux/
https://en.wikibooks.org/wiki/Grep
