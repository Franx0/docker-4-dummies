# Welcome to Node environment, let's start with it:
<center><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Python-logo-notext.svg/100px-Python-logo-notext.svg.png" width="100" height="auto" alt="Python"></center>  
<br>

1. ```> cd pyenv``` in your local cloned directory.
2. Let's build our first image that contains pyenv, Python and Pip versioned installation. Remember, this first step is not going to create the environment right now, it only is going to prepare an image of how the final environment should be.
Get acquainted about Docker syntax, feel free to find out what all it means and try to change the behaviour by your self.

  ### Steps:
  1. ```> cd pyenv```   
  2. ```> docker build -t pyenv .``` 
  3. ```> docker images```  

|REPOSITORY|TAG|IMAGE ID|CREATED|SIZE|    
|---|---|---|---|---|    
|pyenv|latest|f9ca170f5095|1 seconds ago|829MB|  

  4. ```> cd python_3.9```  
  5. ```> docker build -t python_3 .``` 
  6. ```> docker images```  

|REPOSITORY|TAG|IMAGE ID|CREATED|SIZE|    
|---|---|---|---|---|    
|python_3.9|latest|9f3df128f20a|1 seconds ago|1.29GB|  
|pyenv|latest|f9ca170f5095|5 minutes ago|829MB|  

  7. ```> docker run -v python_volume:/shared --name TEST -it -p 8080:8080 python_3.9 bash```  
    Now you will be inside a logged bash terminal with a full pyenv environment set and prepared to start working with python 3.9.0.

  8. Open a new terminal tab and type: ```> docker container ls``` you will see something similar to:  

|CONTAINER ID|IMAGE|COMMAND|CREATED|STATUS|PORTS|NAMES|
|---|---|---|---|---|---|---|
|03f267e27175|python_3.9|"/bin/bash -lc bash"|6 seconds ago|Up 4 seconds|0.0.0.0:8080->8080/tcp, 8080/tcp /tcp|TEST|
