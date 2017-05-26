Note: Text following a pound sign `#` are comments

```
$ cd               # cd without any arguments navigates to the home directory
$ pwd
/home1/03439/wallen
$ mkdir challenge01
$ cd challenge01   
$ mkdir a          
$ mkdir b          
$ mkdir c d e      # make multiple folders simultaneously by providing names seperated by spaces
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
