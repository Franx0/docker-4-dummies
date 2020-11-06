# node_14
This folder includes a Dockerfile to mount Node V14.0.0 version into a Docker container. Please, review Dockerfile annotations to understand the following syntax meanings.  

1. ```> docker run -v node_volume:/shared --name API -it -p 8080:8080 node_14 bash```
2. Inside new opened logging terminal type the following command and check:  
```> pwd``` == ":/shared" 
3. Let's start a new project  
```> mkdir my-api && cd my-api```  
```> cd my-api```
4. Let's create an app.js file:  
```> touch app.js```  
```> 
  echo "
    const http = require('http');
    
    const hostname = '0.0.0.0';
    const port = 8080;
    const server = http.createServer(
      
    (req, res) => {
      res.statusCode = 200;
      res.setHeader('Content-Type', 'text/plain');
      res.end('Hello World');
    });
    
    server.listen(port, hostname, () => {
      console.log(`Server is running in http://${hostname}:${port}/`);
    });
  " > app.js
```  
  
5. Run your local App server:  
```> node app.js```

Visit ```http://localhost:8080``` in your browser and you will see Node server running and message 'Hello World'.  

Because you typed ```> node_volume:/share``` syntax in the docker running container command, you can ends container running state and re-runs again and you will be able to see the previous created project in same directory with all the previous changes.
That is possible because you used a related container Volume which we named node_volume. Feel free to execute:  

```> docker volume ls```  

and you will see the created volume. Volumes are necessary to persist data between containers.  

|DRIVER|VOLUME NAME|  
|---|---|
|local|node_volume|  

> Without using Docker Compose
