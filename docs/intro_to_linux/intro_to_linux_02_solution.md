Note: Text following a pound sign `#` are comments

1) Navigate to your home directory

2) Make a new folder called `challenge01`

3) Navigate into that new folder

```
$ cd               # cd without any arguments navigates to the home directory
$ pwd
/home1/03439/wallen
$ mkdir challenge01
$ cd challenge01   
```

4) Make 5 sub folders called `a`, `b`, `c`, `d`, `e`

```
$ mkdir a          
$ mkdir b          
$ mkdir c d e      # make multiple folders simultaneously by providing names seperated by spaces
```

5) Wihin each of those sub folders, make 5 sub folders called `1`, `2`, `3`, `4`, `5`

```
$ cd a             
$ mkdir 1 2 3 4 5  
$ cd ..            # try to keep in mind your present location as you move through the file system
$ cd b             
$ mkdir 1 2 3 4 5  
$ cd ../c          # use relative paths to navigate up one folder, then into the 'c' folder in one step
$ mkdir 1 2 3 4 5  # use the <UpArrow> to cycle through command history
$ cd ../d          
$ mkdir 1 2 3 4 5  
$ cd ../e          
$ mkdir 1 2 3 4 5  
```

6) Navigate back to your home directory and print a hierarchical view of the `challenge01` folder

```
$ cd ..           
$ pwd              
/home1/03439/wallen/challenge01  
$ cd ..            
$ pwd              
/home1/03439/wallen              
$ tree challenge01 
challenge01                      
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
cd && mkdir challenge01 && cd challenge01; for VAR in a b c d e; do mkdir $VAR && cd $VAR && mkdir 1 2 3 4 5 && cd ../; done; cd && tree challenge01
```


[Return](intro_to_linux_02.md)
