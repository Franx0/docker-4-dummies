# Welcome to Node environment, let's start with it:
<center><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/1200px-Node.js_logo.svg.png" width="250" height="auto" alt="NodeJS"></center>  
<br>

1. ```> cd nvm``` in your local cloned directory.
2. Let's build our first image that contains NVM, NodeJS and NPM versioned installation. Remember, this first step is not going to create the environment right now, it only is going to prepare an image of how the final environment should be.
Get acquainted about Docker syntax, feel free to find out what all it means and try to change the behaviour by your self.

  ### Steps:
  1. ```> cd nvm```   
  2. ```> docker build -t nvm .``` 
  3. ```> docker images```  

|REPOSITORY|TAG|IMAGE ID|CREATED|SIZE|    
|---|---|---|---|---|    
|nvm|latest|d7a06706a2da|1 seconds ago|188MB|  

  4. ```> cd node_14```  
  5. ```> docker build -t node_14 .``` 
  6. ```> docker images```  

|REPOSITORY|TAG|IMAGE ID|CREATED|SIZE|    
|---|---|---|---|---|    
|node_14|latest|690d555c948b|1 seconds ago|398MB|  
|nvm|latest|d7a06706a2da|5 minutes ago|188MB|  

  7. ```> docker run -v node_volume:/shared --name API -it -p 8080:8080 node_14 bash```  
    Now you will be inside a logged bash terminal with a full nvm environment set and prepared to start working with node 14.

  8. Open a new terminal tab and type: ```> docker container ls``` you will see something similar to:  

|CONTAINER ID|IMAGE|COMMAND|CREATED|STATUS|PORTS|NAMES|
|---|---|---|---|---|---|---|
|b78e641b408f|node_14|"/bin/bash -lc bash"|6 seconds ago|Up 4 seconds|0.0.0.0:8080->8080/tcp|API|
