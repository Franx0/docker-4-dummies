# python_3.9
This folder includes a Dockerfile to mount Python 3.9.0 version into a Docker container. Please, review Dockerfile annotations to understand the following syntax meanings.  

1. ```> docker run -v python_volume:/shared --name TEST -it -p 8080:8080 python_3.9 bash```
2. Inside new opened logging terminal type the following command and check:  
```> pwd``` == ":/shared" 
3. Let's start a new project in there.

Because you typed ```> python_volume:/share``` syntax in the docker running container command, you can ends container running state and re-runs again and you will be able to see the previous created project in same directory with all the previous changes.
That is possible because you used a related container Volume which we named python_volume. Feel free to execute:  

```> docker volume ls```  

and you will see the created volume. Volumes are necessary to persist data between containers.  

|DRIVER|VOLUME NAME|  
|---|---|
|local|python_volume|  

> Without using Docker Compose
