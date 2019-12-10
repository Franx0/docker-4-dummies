## Welcome to Rails environment, let's start with it: ##
<center><img src="https://upload.wikimedia.org/wikipedia/commons/6/62/Ruby_On_Rails_Logo.svg" width="233" height="196" alt="RubyOnRails"></center>

1. ```> cd rails```
2. Let's build our first image that contains RVM, Ruby, Rails and Node versioned installation. Remember, this first step is not going to create the environment right now, it only is going to prepare an image of how the final environment should be.
Get acquainted about Docker syntax, feel free to find out what all it means and try to change the behaviour by your self.

# Steps: #  
1. ```> cd rails```   
2. ```> docker build -t rvm .```  
3. ```> cd rails_6```  
4. ```> docker build -t rails_6```  
5. ```> cd {any directory}```  
6. ```> docker run -v rails_volume:/shared -it -p 3000:3000 rails_6 bash```  

Now you will be inside a logged bash terminal with a full rvm environment set and prepared to start working with rails 6.

# rails_6 (Example) #
This folder includes a Dockerfile to mount Rails 6 version into a Docker container. Please, review Dockerfile annotations to understand the following syntax meanings.

1. ```> pwd``` == ":/shared"  
2. ```> rails new rails-api-project --api```  
3. ```> cd rails-api-project```
4. ```> rails s -b 0.0.0.0```  

Visit localhost:3000 in your browser and you will see Rails initial Welcome Page running. 
Because you typed ```> rails_volume:/share``` syntax in the docker running container command, you can ends container running state and re-runs again and you will be able to see the previous created project in same directory with all the previous changes.
That is possible because you used a related container Volume which we named rails_volume. Feel free to execute:  

```> docker volume ls```  

and you will see the created volume. Volumes are necessary to persist data between containers.  

|DRIVER|VOLUME NAME|  
|---|---|
|local|rails_volume|  

> Without using Docker Compose
