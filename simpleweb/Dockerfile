# Specify a base image
# FROM alpine # 1st error, original alpine image doesn't contain npm
FROM node:alpine

# 2nd error, we'll get the error before we add a WORKDIR and COPY commands
## the first ./ is path to folder to copy from on our machine relative to build context "docker build ." which is simpleweb folder
## the second ./ is location to copy stuff to inside the container
### run "docker run -it <image id> sh"
### the WORKDIR command is used to declare our working directory in the container so when we copy file from the the first ./
### to the second ./ then the second one will be directed to our new set working directory which is /usr/app. If the /usr/app
### directory is not exist inside the container, it will be automatically created for us
WORKDIR /usr/app
COPY ./ ./
# COPY ./package.json ./

# Install some dependencies
RUN npm install

# COPY ./ ./

# Default command
CMD [ "npm","start" ]