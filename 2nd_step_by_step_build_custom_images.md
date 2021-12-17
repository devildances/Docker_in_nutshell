# BUILDING CUSTOM IMAGES THROUGH DOCKER SERVER

<img src="/files/images/img7.png" height="55%" width="55%" />

A Dockerfile is essentially a plain text file that is going to have a couple of line of configuration placed inside of it. This configuration is going to define how our container behaves or more specifically what different programs it's going to contain and what it does when it starts up as a container.


<img src="/files/images/img8.png" height="35%" width="35%" />

- inside of every Dockerfile, we're always going to specify a base image
- after that we'll add in some additional configuration to run commands, to add in some dependencies or some more software, some more programs that we need to successfully create and execute our container
- and finally, we'll specify a startup command for the image
    - so anytime we take that image and create a container out of it, it will be the command that is executed to essentially boot up or start the container



### Example 1 - Create an image that runs redis-server

<img src="/files/images/img9.png" height="40%" width="40%" />

```Dockerfile
FROM alpine

RUN apk add --update redis

CMD ["redis-server"]
```

<img src="/files/images/img10.png" height="40%" width="40%" />

- `FROM`
    - this is used to specify the image that we want to use as a base
    - by putting `FROM alpine`  means we want to use as a base image of Alpine when preparing our image
- `RUN`
    - this is used to execute some commands while we are preparing our custom image
- `CMD`
    - it specifies what should be executed when our image is used to start up as a brand new container

The corresponding file is under *redis-image* folder in this directory, the ways how we run the Dockerfile as the following:

- go to the terminal and direct to the corresponding folder directory
- run ```docker build .``` command
- once the image already built, then copy the image ID and run ```docker run <image id>``` commmand



## Tagging an Image

<img src="/files/images/img11.png" height="40%" width="40%" />
<img src="/files/images/img12.png" height="40%" width="40%" />

Based on the *Example 1* above, we can run the following command to give a tag/name of our final image from `docker build` rather than image ID everytime we run that image to build a container:

```bash
docker build -t devildances/redis:1.0.0 .
```