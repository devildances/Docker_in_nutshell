# Making 1st Simple Project

<img src="/files/images/img13.png" height="40%" width="40%" />

Goal of this sample project is to create a tiny Node JS Web App application, warp it inside of a docker container and then be able to access that web apps from a browser running on our local machine.


These are a quick outline of some of the steps that we're going to go through :

<img src="/files/images/img14.png" height="40%" width="40%" />


> This project is contained in *simpleweb* folder.

- Create Node JS web app
    - Create *package.json* file
        - this file contains a little bit of configuration to describe how our Node app is going to work exactly
    - Create *index.js* file
- Create a Dockerfile
    - <img src="/files/images/img15.png" height="40%" width="40%" />
    - the series of operations that we're going to put into the Dockerfile is going to end up looking very similar to what we did in *2nd_step_by_step_build_custom_images.md* file for Redis application
- Build image from Dockerfile
    - run `docker build -t <docker ID>/<project name>:<version> <working directory>` command
        - `docker build -t devildances/simpleweb .`
- Run image as container
    - <img src="/files/images/img16.png" height="40%" width="40%" />
    - for this case we're not only running simple `docker run <docker ID>/<project name>:<version>` command but `docker run -p <port outside container>:<port inside container> <image ID>` command since we need **Port Mapping** to our container so we can open the nodejs app thorugh our web browser
        - `docker run -p 8080:8080 devildances/simpleweb`
- Connect to web app from a web browser
    - open the web browser and go to the localhost:8080 address
- **Start a shell inside the running container using** `docker exec -t <container ID> sh` **command instead of running** `docker run -it <image id> sh` **command**
    - run `docker ps` to get the container ID
    - run `docker exec -t <container ID> sh` command