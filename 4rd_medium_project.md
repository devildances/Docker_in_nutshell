# Build Multiple Local Containers

The purpose of this application is to make a Docker container that contains a Web application that simply displays inside the browser the number of times that someone essentially has essentially visited the server.

In order to build this, we're going to need 2 separates components.

<img src="/files/images/img17.png" height="40%" width="40%" />

1. First off, we're going to need some type of Web server, something to actually respond to HTTP requests and gegerate some HTML to show inside the browser
2. To actually store the number of times that Web apps page has been visited, we're going also make use of a little Redis server
    - The only purpose of Redis server is going to be to contain the number of times that the page has been visited

<img src="/files/images/img18.png" height="40%" width="40%" />


> This project is contained in *visits* folder.


- Create Node JS web app
    - Create *package.json* file
        - this file contains a little bit of configuration to describe how our Node app is going to work exactly
    - Create *index.js* file
- Create a Dockerfile for our Node app
- Create a **Docker Compose** file
    - <img src="/files/images/img19.png" height="40%" width="40%" />
        - Since we want to connect between 2 separate containers so we need to use Docker compose
        - Those 2 containers are 2 abosolutely isolated processes that don't have any communication so in order to make sure that our Node app has the ability to kind of reach out to the Redis server we need to set up some networking infrastrucure between them which we can do that in Docker compose file
        - Docker Compose is going to make it very easy and very straightforward to start up multiple Docker containers at the same time and automatically connect them together with some form of networking
    - <img src="/files/images/img20.png" height="40%" width="40%" />
        - To make use of Docker Compose, we're essentially gonna take the same commands that we were running before like `docker build` and `docker run` but we're going to kind of encode these commands into a very special file in our project directory called *docker-compose.yml*
        - Once we create the file, then feed it into the `docker-compose CLI` and it'll be up to the CLI to parse that file and create all the different containers with the correct configuration that we specified
    - <img src="/files/images/img21.png" height="40%" width="40%" />
        - As per image above, that's essentially we're going to write into the YAML file
        - The details on the file
        - `version`
            - it's the specific version of Docker compose that we want to use
        - `services`
            - it's essentially saying a type of container and we define 2 services
                - `redis-server`
                    - it's the name for our Redis container and it can be anything
                    - `image: 'redis'`
                        - it contains the image name that Docker compose will use to create this service/container
                - `node-app`
                    - it's the name for our Node app container and it can be anything
                    - `build: .`
                        - means we want this container to be built using the Dockerfile inside the current directory of the project
                    - `ports`
                        - it's used to specify all the different ports that we want to be opened up on this service/container
                        - `- "4001:8081"`
                            - `<outside port>:<inside port>`
                            - with the dash in YAML file we can technically map many different ports inside of a single Docker compose file for a single service/container, but in our case we only want to map 1 set of ports
                            - here we're going to connect port 4001 on our local machine to 8081 inside the container
- Build the images from YAML file using Docker Compose command
    - <img src="/files/images/img22.png" height="40%" width="40%" />
        - The commands are pretty similar with Docker default command when we want to build a container based on Dockerfile
    - run `docker-compose up` command
    - or run `docker-compose up --build` command
- Connect to web app from a web browser
    - open the web browser and go to the localhost:4001 address
- Stop multiple Docker compose containers
    - <img src="/files/images/img23.png" height="40%" width="40%" />
- This is how we deal with containers that crash for some given reason
    - <img src="/files/images/img24.png" height="40%" width="40%" />
        - This is how we're going to get Docker compose to automatically restart a container using **Restart Policy** inside our YAML file for specific service/container
        - There are 4 types of **Restart Policy**
            - `"no"` or `'no'`
                - it means if a container crashes for any reason then do not attempt to restart it
                - if we set the restart parameter using this value, we need to add double/single quotes before and after the value
            - `always`
                - it means if the container stops for absolutely any reason whatsoever, automatically attempt to restart it
            - `on-failure`
                - it means it only going to attempt to restart the running container if we get an error code (other than 0 value)
            - `unless-stopped`
                - it means always attempt to restart a container unless we at the command line forcibly tell that container to stop by running `docker stop`
- Check container status using Docker compose
    - `docker-compose ps`
    - when we run this command, it's going to specifically look for *docker-compose.yml* fileinside our current directory and if it finds one then it'll read that file and will try to find all of the running containers on our local machine that belong essentially to that YAML file
- **Start a shell inside the running container using** `docker exec -t <container ID> sh` **command instead of running** `docker run -it <image id> sh` **command**
    - run `docker ps` to get the container ID
    - run `docker exec -t <container ID> sh` command