# Lab Report 3

## The grep Command
Let's say we have the skill-demo1-data repository on our local computer. We can retrieve it by doing `git clone https://github.com/ucsd-cse15l-w23/skill-demo1-data`. Here we can use the grep command to search and match through directories and files in the skill-demo1-data repo, using a specific pattern that we want to search for.

## The Recursive Option
The `-r` stands for recursive. This means that the command recursively goes through each file in the repository looking for the string that matches the one listed string, or "pattern". For example, we can use the grep option like this in the skill-demo1-data repository on the home directory (in the skill-demo1-data folder).<br>
Input:
```
grep -r 'Ringsend'
```
Output:
```
written_2/travel_guides/berlitz1/WhatToDublin.txt:        the RDS. Greyhound racing is on at Shelbourne Park, Ringsend, and at
written_2/travel_guides/berlitz1/WhereToDublin.txt:        Grand Canal Basin, Ringsend, off Pearse Street, Dublin
```
The command recursively looks for all content in each file in all of the folders, starting from the current directory path. It looks for the word "Ringsend" throughout all the content and outputs the file paths and part of the content that contains the word in context. This is extremely helpful because otherwise, we would need to state a single file path in the grep command like `grep 'Ringsend' file/path`. The recursive option lets us look at multiple files instead of just one. Another example shows if we use two words. <br>
Input:
```
grep -r 'rive droite'
```
Output:
```
written_2/travel_guides/berlitz2/Paris-WhereToGo.txt:The sprawling Right Bank (rive droite) covers the whole range of Paris’s social life, from ultra-chic to downright sleazy. It claims the most luxurious shopping areas, the presidential Elysée Palace, the grands boulevards and financial district, but also, farther north, seamy Clichy and Pigalle, as well as hilly Montmartre, where modern art could be said to have begun. Back in the middle of it all, the huge Louvre museum makes its own magnificent statement. Just to the east, Les Halles, Beaubourg (around the Centre Georges-Pompidou), and place de la Bastille have each been transformed by controversial projects. The variety and energy of the nightlife here has overtaken that of the Left Bank. Even the charming old Marais and its Jewish quarter, representing the old Paris of the 17th century, have taken on a new fashionable appearance with the influx of trendy boutiques.
```
Here we can see that we can recursively look for two words right next to each other. In this way, we can search for entire phrases or sentences. <br>
Source: [[Link](https://www.gnu.org/software/grep/manual/grep.html)](https://www.gnu.org/software/grep/manual/grep.html)

## The Files with Matches Option
The `-l` option suppresses the normal output by only printing the file name, not the context for which the word is in. Therefore, it does not show the content of any files.<br>
Input:
```
grep 'tower' ./written_2/travel_guides/berlitz2/Paris-WhereToGo.txt -l
```
Output:
```
./written_2/travel_guides/berlitz2/Paris-WhereToGo.txt
```
Here the option is not very helpful because we already know the file that we are using grep on (as we had to type it out in the first place). However, the output does not show where 'tower' is used, which makes the output much less cluttered than it would be without `-l`. In fact, tower is shown 16 times. The commands above in the `-r` section show very cluttered outputs. Only showing filenames is especially helpful when we recursively go through multiple files. We can pair this option with the `-r` option.<br>
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
Here every file is checked recursively for 'Dublin'. Instead of printing out all the content for each file, it only shows file names. This is many files, so it would look much more convoluted without the `-l` option. <br>
Source: https://man7.org/linux/man-pages/man1/grep.1.html

## The Ignore Case Option
The `-i` option ignores the case of the pattern that you are searching for. This means that uppercase and lowercase letters are searched for interchangeably, even if your input string is all lowercase or all uppercase. This is important when looking for a word that can be used in both uppercase and lowercase throughout a file (or multiple files).<br>
Input:
```
grep 'treasure' written_2/travel_guides/berlitz2/Cuba-WhereToGo.txt -i
```
Output:
```
Havana was founded along a vast natural harbor in 1519. During the 16th century a fleet of galleons laden with treasures used the port as a pit stop on the way back to Spain from the New World. By the 17th century pirate attacks prompted the building of extensive city defenses — colossal forts, a chain across the harbor mouth, and prominent city walls — making Havana the “Bulwark of the West Indies.”
Continuing west along Calle Oficios, you’ll come to a splendidly restored square, Plaza de San Francisco, with upscale shops, restaurants, and the imposing 18th-century Iglesia y Convento de San Francisco de Asís. The convent contains a museum with Spanish treasures, and you can climb the belltower for spectacular views of Old Havana. Concerts are frequently held here. Nearby, you’ll find several impeccable colonial-era houses with brilliantly colored façades.
The Isla de la Juventud (Isle of Youth) is Cuba’s largest offshore island, some 50 km (31 miles) in diameter, but not its prettiest. It is said to have been the location for Robert Louis Stevenson’s Treasure Island; pirates once buried their booty here. The island received its jaunty name in the 1970s, when as many as 22,000 foreign students (mainly from politically sympathetic African countries) studied here in no fewer than 60 schools.
A more appealing prospect is picturesque Guamá, a half-hour boat ride from La Boca along an artificial channel and then across the vast Laguna del Tesoro (Treasure Lake). Legend has it that the Indians dumped their jewels into the water rather than surrender them to Spanish conquistadores. Guamá is a group of tiny islands connected by wooden bridges. A few visitors stay in the thatched cabañas (see page 131), but most just come to wander along the boardwalk, greet the ducks and egrets, and have a meal.
Aimless wandering is especially fruitful in Trinidad — and, since dozens of street names have changed and neither maps nor residents seem sure of what to call many of them, roaming without a plan is the only practical solution. Virtually every street is its own colonial treasure and feast for the eyes. Near the bus station, you might stumble across the musical septet “Los Pinos” jamming in the street, just out of reach of kids playing stickball. Farther afield, southeast along Calle J. M. Márquez, you’ll find Ermita de Santa Ana, a bricked-up church overlooking the town on a hill where boys fly homemade kites.
Many visitors prefer Cuba’s second city (population 420,000) to the capital. Santiago de Cuba (880 km/546 miles southeast of Havana) is unpolished, has few grand palaces, and cannot compare with the colonial treasures found in Havana and Trinidad. But it is unfailingly vibrant and seductive, exuding a feel all its own. Enclosed by the Sierra Maestra mountains, Santiago can also be wickedly hot. Santiagueros negotiate their hilly streets by keeping to the shady sides, and they relax with little urgency on overhanging balconies.
```
The output shows all parts of the file where 'treasure' is shown. However, the difference between using `-i` and not using `-i` is that parts that have an uppercase 'Treasure', such as when the file says "Robert Louis Stevenson’s Treasure Island", will not be shown unless the `-i` option is used. This is very important as names are almost always uppercase at the starting letter. <br>
Input:
```
grep 'dublin' -r -l -i
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
Here we are using all of the options we learned so far. We recursively (`-r` option) look through the contents of each file for the word 'dublin'. However, the ignore case option means that we do not care about uppercases or lowercases, so it will also include 'Dublin", or even 'DuBlIn" (if that ever showed up). Then we only print the filenames so the output is less cluttered (`-l` option). If we did not use `-i`, then nothing would show up on the output because the word 'dublin' in all lowercase never shows up, only 'Dublin' does. <br>
Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

## The Count Option
The `-c` option is a very convenient option that servers the purpose of the `wc` command when using grep by only showing the number of times the pattern comes up (number of lines that the pattern shows up in).<br>
Input:
```
grep 'France' -c written_2/travel_guides/berlitz1/IntroFrance.txt
```
Output:
```
13
```
A longer way we can find how many lines have the word "France" in the IntroFrance.txt file is by piping the output from grep over to the `wc` command, like this: `grep 'France' written_2/travel_guides/berlitz1/IntroFrance.txt | wc`. This will output `     13     137     942`, showing that "France" came up in 13 lines. Now, traverse to the written2/travel_guides/berlitz2 file by doing `cd written2/travel_guides/berlitz2`. <br>
Input:
```
grep 'tree' -i -r -c
```
Ouput:
```
Algarve-History.txt:1
Algarve-Intro.txt:0
Algarve-WhatToDo.txt:11
Algarve-WhereToGo.txt:20
Amsterdam-History.txt:0
Amsterdam-Intro.txt:7
Amsterdam-WhatToDo.txt:11
Amsterdam-WhereToGo.txt:20
Athens-History.txt:1
Athens-Intro.txt:2
Athens-WhatToDo.txt:8
Athens-WhereToGo.txt:16
Bahamas-History.txt:0
Bahamas-Intro.txt:0
Bahamas-WhatToDo.txt:6
Bahamas-WhereToGo.txt:22
Bali-History.txt:0
Bali-WhatToDo.txt:1
Bali-WhereToGo.txt:28
Barcelona-History.txt:0
Barcelona-WhatToDo.txt:5
Barcelona-WhereToGo.txt:38
Beijing-History.txt:1
Beijing-WhatToDo.txt:11
Beijing-WhereToGo.txt:22
Berlin-History.txt:1
Berlin-WhatToDo.txt:3
Berlin-WhereToGo.txt:9
Bermuda-WhatToDo.txt:3
Bermuda-WhereToGo.txt:28
Bermuda-history.txt:0
Boston-WhereToGo.txt:55
Budapest-History.txt:0
Budapest-WhatToDo.txt:2
Budapest-WhereoGo.txt:22
California-History.txt:1
California-WhatToDo.txt:7
California-WhereToGo.txt:47
Canada-History.txt:0
Canada-WhereToGo.txt:92
CanaryIslands-History.txt:1
CanaryIslands-WhatToDo.txt:2
CanaryIslands-WhereToGo.txt:20
Cancun-History.txt:1
Cancun-WhatToDo.txt:2
Cancun-WhereToGo.txt:14
China-History.txt:2
China-WhatToDo.txt:1
China-WhereToGo.txt:50
Costa-History.txt:0
Costa-WhatToDo.txt:0
Costa-WhereToGo.txt:15
CostaBlanca-History.txt:0
CostaBlanca-WhatToDo.txt:2
Crete-History.txt:1
Crete-WhatToDo.txt:8
Crete-WhereToGo.txt:23
CstaBlanca-WhereToGo.txt:17
Cuba-History.txt:1
Cuba-WhatToDo.txt:4
Cuba-WhereToGo.txt:32
Nepal-History.txt:5
Nepal-WhatToDo.txt:9
Nepal-WhereToGo.txt:23
NewOrleans-History.txt:3
Paris-WhatToDo.txt:1
Paris-WhereToGo.txt:24
Poland-History.txt:2
Poland-WhatToDo.txt:1
Portugal-History.txt:0
Portugal-WhatToDo.txt:4
Portugal-WhereToGo.txt:38
PuertoRico-History.txt:1
PuertoRico-WhatToDo.txt:6
PuertoRico-WhereToGo.txt:22
Vallarta-History.txt:1
Vallarta-WhatToDo.txt:1
Vallarta-WhereToGo.txt:12
```
Here is an interesting usage of `-c` that is hard to replicate using `wc`. Essentially, from berlitz2, we recursively checked the content of each file for the word "tree", ignoring the case with the `-i` option. The count option does not show the context for which the word appears, however, it shows the number of times that the word has shown up in each file in berlitz2, even if it shows up 0 times. This is very helpful for seeing which files contain the most or least of a specific pattern. <br>
Source: https://en.wikibooks.org/wiki/Grep

## Sources
`man grep` shows helpful options and a description of grep. <br>
https://www.gnu.org/software/grep/manual/grep.html<br>
https://man7.org/linux/man-pages/man1/grep.1.html<br>
https://www.geeksforgeeks.org/grep-command-in-unixlinux/<br>
https://en.wikibooks.org/wiki/Grep<br>
