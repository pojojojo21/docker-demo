# Docker Demo

Let's learn some docker.

## Installation

[Install Docker](https://docs.docker.com/get-docker/)

## Demo 1 - Running

### Toying Around

Pull your image and check out the layers!

```
$ docker pull ubuntu:latest
latest: Pulling from library/ubuntu
da7391352a9b: Pull complete 
14428a6d4bcd: Pull complete 
2c2d948710f2: Pull complete 
Digest: sha256:c95a8e48bf88e9849f3e0f723d9f49fa12c5a00cfc6e60d2bc99d87555295e4c
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

Now run it and play around in the container (ls, cd, cat, etc):

```
$ docker run -it --rm ubuntu /bin/bash
```

In another terminal, look at your active containers:


```
$ docker ps -a
```

You can close out of your open container, but before continuing, make sure all your containers have been cleaned up! This should have been handled via the `--rm` flag, but run `docker ps -a` to check. If you have any extras, you can use `docker rm` to delete them.

### Using an image

Run the 2048 docker image:

```
$ docker run -it --rm alexwhen/docker-2048
```

This application exposes 2048 on port 80. Can you figure out how to expose the port on port 8080 on your machine? The [docker documentation](https://docs.docker.com/engine/reference/commandline/cli/) might help.

If you have extra time right now, play around with some of the docker run flags. Some fun ones are `-v`, `-d`, `--name`, etc. You can check out the docker documentation for info on how these work. Also, you can google around and see if there are other interesting images. Maybe `python` or `node`?

## Demo 2 - Building

We've provided you with a blank Dockerfile containing only a base `nginx` image. [Nginx](https://www.nginx.com/) is a high-performance load balancer and webserver used across the industry. While Nginx has a complex feature set, all we need you to do is have it serve the static html files in the `static/` directory.

There are many ways to do this, but we'd recommend using the `COPY` directive. How to use and where to copy to is an excercise left up to you, though! Maybe reading the [nginx Docker Hub docs](https://hub.docker.com/_/nginx) will be helpful.

Once you think you've got the Dockerfile right, use `docker build . -t nginx-demo` to build the container to the name `nginx-demo`.

When you've got the image built, try to run the container! Remember that the `nginx` image runs on port 80. Is there a way (using syntax you've already learned) to bind port 8080 on your machine to port 80 on the container?

If the container is running successfully, go to `localhost:8080` in your browser to see if it worked!

If you've got some extra time here, you've got a few options:

1. Play 2048
2. Try to get live webpage reloading working using volume binding instead of COPY
3. Go for the extra credit below

### Extra Credit - Reverse Proxy

While Nginx can be used as a standalone webserver, it's usually used as a [reverse proxy](https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy/) (load balancer) in industry.

For extra credit, implement the following behavior using only the docker CLI and the nginx configuration file:

- If the webserver is accessed at any normal path, serve the website we've given to you here.
- If the webserver is accessed at the path `/2048`, forward the request to the `2048` container.

Concretely, if you go to `localhost:8080` in your browser, you should see the site we gave you. If you go to `localhost:8080/2048`, you should see 2048.

The first group (2 people) to implement this behavior will get 10 points extra credit on the docker homework!
