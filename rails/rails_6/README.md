# rails_6
This folder includes a Dockerfile to mount Rails 6 version into a Docker container. Please, review Dockerfile annotations to understand the following syntax meanings.  

1. ```> docker run -v rails_volume:/shared --name API -it -p 3000:3000 rails_6 bash```
2. Inside new opened logging terminal type the following command and check:  
```> pwd``` == ":/shared"  
3. Let's create a new Rails Api project:  
```> rails new rails-api-project --api```  
4. Move inside new Rails project directory:  
```> cd rails-api-project```
5. Run your local Rails server:  
```> rails s -b 0.0.0.0```

Visit ```http://localhost:3000``` in your browser and you will see Rails initial Welcome Page running.  

Because you typed ```> rails_volume:/share``` syntax in the docker running container command, you can ends container running state and re-runs again and you will be able to see the previous created project in same directory with all the previous changes.
That is possible because you used a related container Volume which we named rails_volume. Feel free to execute:  

```> docker volume ls```  

and you will see the created volume. Volumes are necessary to persist data between containers.  

|DRIVER|VOLUME NAME|  
|---|---|
|local|rails_volume|  

> Without using Docker Compose
