
1) Extract every word from `websters.txt` that contains the string `apple`, and put it into a new file called `apple.txt`.
```
$ pwd
/home1/03439/wallen
$ cd IntroToLinuxHPC/Lab01
$ grep "apple" websters.txt > apple.txt
```


2) Extract every word from `websters.txt` that contains the string `carrot`, and put it into a new file called `carrot.txt`.
```
$ grep "carrot" websters.txt > carrot.txt
```


3) Extract every word from `websters.txt` that contains the string `cheese`, and put it into a new file called `cheese.txt`.
```
$ grep "cheese" websters.txt > cheese.txt
```


4) Examine the contents of `apple.txt`, `carrot.txt`, and `cheese.txt` to make sure they contain what you expect.
```
$ cat apple.txt            # Different methods of examining file contents are appropriate depending
$ more carrot.txt          # on the size of the file. Try different combinations to see what works.
$ less cheese.txt
```


5) Concatenate all three lists into a new file called `food.txt`.
```
$ cat apple.txt > food.txt     # this will create the file 'food.txt' if it does not yet exist
$ cat carrot.txt >> food.txt   # Double >> to append, not overwrite
$ cat cheese.txt >> food.txt

$ more food.txt
```


6) Advanced Linux users: can you do all of the above, and alphabetize the output in one command?
```
$ grep -E 'apple|carrot|cheese' websters.txt  | sort > food.txt
```

[Return](intro_to_linux_04.md)

