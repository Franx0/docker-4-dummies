# Welcome to Rails environment, let's start with it:
<center><img src="https://upload.wikimedia.org/wikipedia/commons/6/62/Ruby_On_Rails_Logo.svg" width="233" height="196" alt="RubyOnRails"></center>

1. ```> cd rvm``` in your local cloned directory.
2. Let's build our first image that contains RVM, Ruby, Rails and Node versioned installation. Remember, this first step is not going to create the environment right now, it only is going to prepare an image of how the final environment should be.
Get acquainted about Docker syntax, feel free to find out what all it means and try to change the behaviour by your self.

  ### Steps:
  1. ```> cd rvm```   
  2. ```> docker build -t rvm .``` 
  3. ```> docker images```  

|REPOSITORY|TAG|IMAGE ID|CREATED|SIZE|    
|---|---|---|---|---|    
|rvm|latest|17f83aa768dd|1 seconds ago|190MB|  

  4. ```> cd rails_6```  
  5. ```> docker build -t rails_6 .``` 
  6. ```> docker images```  

|REPOSITORY|TAG|IMAGE ID|CREATED|SIZE|    
|---|---|---|---|---|    
|rails_6|latest|285d8172e03e|1 seconds ago|561MB|  
|rvm|latest|17f83aa768dd|5 minutes ago|190MB|  

  7. ```> docker run -v rails_volume:/shared --name API -it -p 3000:3000 rails_6 bash```  
    Now you will be inside a logged bash terminal with a full rvm environment set and prepared to start working with rails 6.

  8. Open a new terminal tab and type: ```> docker container ls``` you will see something similar to:  

|CONTAINER ID|IMAGE|COMMAND|CREATED|STATUS|PORTS|NAMES|
|---|---|---|---|---|---|---|
|b78e641b408f|rails_6|"/bin/bash -lc bash"|6 seconds ago|Up 4 seconds|0.0.0.0:3000->3000/tcp|API|
