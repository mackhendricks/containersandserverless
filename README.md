# Contain Yourself: Containers and Serverless

## Prereq's

### Install Docker on MacOS

https://docs.docker.com/get-docker/

## The Basics & Review for Some: 

### Hello World 

**Download Docker Image and Run It**

```
docker run -p 8888:80 mackhendricks/static-site
```

**Open a web browswer and point to** 

http://localhost:8888

**Kill/Stop the Image**

Enter Control-C

**Run the container in the background**

```
docker run -d -p 8888:80 mackhendricks/static-site
```

Docker will generated a container ID.  It will look something lke this

```
3ba42b3f8366e00bf8866b3b863eb3228d97090c81488648d60da5bab00e203
```
**Open a web browswer and point to** 

http://localhost:8888

**Lets look at the running image**

```
docker ps
```

It only shows you the first 12 digits of the image id for readability purposes

### Inspect Hello World Container


### Build Our Own

Use Case: 

We have an application the will be built by a team of 5 people. The development team has selected Python and they have a set of dependencies that should be installed in each persons development environment.

- Step 1: Figure out the base image
- Step 2: Setup Python and the Requirements file
- Step 3: Setup ENV variables to allow developers to provide state to the container and/or enable the deployment pipeline
- Step 4: Configure it so that the development team can mount their instance of the repo into the container

## Push IT

## Deploy IT 

## Why Do Any of This? Go Serverless!

## Resources

Serverless Basics: https://serverless-stack.com/chapters/what-is-serverless.html
