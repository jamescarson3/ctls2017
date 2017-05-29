Note: Text following a pound sign `#` are comments

1) Navigate to your home directory

2) Make a new folder called `challenge02`

3) Navigate into that new folder

```
$ cd               # cd without any arguments navigates to the home directory
$ pwd
/home1/03439/wallen
$ mkdir challenge02
$ cd challenge02
```

4) Make 5 sub folders called `a`, `b`, `c`, `d`, `e`

```
$ mkdir a          
$ mkdir b          
$ mkdir c d e      # make multiple folders simultaneously by providing names seperated by spaces
```

5) Wihin each of those sub folders, make 5 files called `1`, `2`, `3`, `4`, `5`

```
$ cd a             
$ touch 1 2 3 4 5  
$ cd ..            # try to keep in mind your present location as you move through the file system
$ cd b             
$ touch 1 2 3 4 5  
$ cd ../c          # use relative paths to navigate up one folder, then into the 'c' folder in one step
$ touch 1 2 3 4 5  # use the <UpArrow> to cycle through command history
$ cd ../d          
$ touch 1 2 3 4 5  
$ cd ../e          
$ touch 1 2 3 4 5  
```

6) Navigate back to your home directory and print a hierarchical view of the `challenge02` folder

```
$ cd ..           
$ pwd              
/home1/03439/wallen/challenge02  
$ cd ..            
$ pwd              
/home1/03439/wallen              
$ tree challenge02 
challenge02                      
|-- a                            
|   |-- 1                        
|   |-- 2                        
|   |-- 3                        
|   |-- 4                        
|   `-- 5                        
|-- b                            
|   |-- 1                        
|   |-- 2                        
|   |-- 3                        
|   |-- 4                        
|   `-- 5                        
|-- c                            
|   |-- 1                        
|   |-- 2                        
|   |-- 3                        
|   |-- 4                        
|   `-- 5                        
|-- d                            
|   |-- 1                        
|   |-- 2                        
|   |-- 3                        
|   |-- 4                        
|   `-- 5                        
`-- e                            
    |-- 1                        
    |-- 2                        
    |-- 3                        
    |-- 4                        
    `-- 5                        
```

7) Advanced Linux users: can you do this on one line?

```
cd && mkdir challenge02 && cd challenge02; for VAR in a b c d e; do mkdir $VAR && cd $VAR && touch 1 2 3 4 5 && cd ../; done; cd && tree challenge02
```


[Return](intro_to_linux_03.md)
