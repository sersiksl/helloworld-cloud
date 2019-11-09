# Docker Beginner Tutorial

Disclaimer: This tutorial heavily borrows from: [https://developer.ibm.com/tutorials/building-docker-images-locally-and-in-cloud/](https://developer.ibm.com/tutorials/building-docker-images-locally-and-in-cloud/)

In this tutorial you will learn:

(1) How to start a container
(2) The difference between an image and a container
(3) Container are epheremal
(4) How to write an easy Dockerfile
(5) How to persist data created in container 

Even this is a beginner tutorial it expects you to have Docker installed on your computer. If you need help to install Docker, please have a look at [intro-docker-requirements](../intro-docker-requirements)

## First Docker Container

Now let's try to start our first container that is based on a centos image:

```bash
docker run -it centos:latest /bin/bash
```

As this runs, let’s talk about what’s happening. When you run the docker command, you’re telling Docker that you want the latest copy from the public Docker hub and run it with the shell of /bin/bash. The command runs off to the Internet, sees the version you have, checks against either the SHA of your cached image, or if you don’t have it, pulls it down from Dockerhub. For clarity’s sake, the -it runs it as interactive and creates a tty for the container. You should see the following now:

```bash
Unable to find image 'centos:latest' locally
latest: Pulling from library/centos
a02a4930cb5d: Pull complete
Digest: sha256:184e5f35598e333bfa7de10d8fb1cebb5ee4df5bc0f970bf2b1e7c7345136426
Status: Downloaded newer image for centos:latest
[root@2de726a5fcb8 /]#
```

Congratulations! You now have your first running Docker container.

## Container vs. Image

So we used the centos image to start our container. What is the difference between an image and a container?

- Docker Images are read-only templates, from which container are instantiated
- Docker Images consist of one or more layer
- Docker Container add an writable layer on top of the images' layer
- One Docker Image can be used in more than one container at the same time

In short: Docker Container = Docker Image + writable Layer

If you would like to learn more about images, containers and layers, please have a look at: [https://docs.docker.com/storage/storagedriver/](https://docs.docker.com/storage/storagedriver/).

## Container and (non)persistence

Go ahead and type exit, and run that docker command again.

```bash
[root@2de726a5fcb8 /]# exit
exit
$ docker run -it centos:latest /bin/bash
[root@583c6cec5d41 /]#
```

Notice how the roots @2de726a5fcb8 and @583c6cec5d41 are different? It’s because when you spin up containers this way they are ephemeral. Ephemeral means they only live for the time that they are running, so as soon as you exit it goes away. We’ll show you how to do longer lived containers in a little while.
Now let’s play around in the container for a second. Being a CentOS machine, the package manager yum is available. Let's use it to install the editor vim.

```bash
[root@583c6cec5d41 /]# yum install vim
```

Now you can run vim in your container! Try it out.

```bash
 [root@583c6cec5d41 /]# vim
````

If you don’t know how to exit vim, type: :q and you should see your command prompt again.

Now type exit again to exit the container.

```bash
[root@583c6cec5d41 /]# exit
exit
```

Start the container again:

```bash
$ docker run -it centos:latest /bin/bash
[root@86f1f3872cbe /]# vim
bash: vim: command not found
[root@86f1f3872cbe /]# exit
exit
$
```

And just to reinforce, when your container is gone any and all changes inside it are gone, too. In this case there is no vim editor.

## Dockerfile

Okay, so we can spin up a container and make changes to it, but how do we keep changes around? There are a few ways to do this, we will show you the most common way to achive this: by using a Dockerfile.

Back at your command prompt, make a new directory and change the directory by using your $EDITOR of choice to open a new file called Dockerfile.

```bash
$ mkdir docker-tutorial
$ cd docker-tutorial
$ $EDITOR Dockerfile
```

We’ll hit the highlights of Dockerfiles here, but we strongly suggest you take a look at [the documentation][dockerfile] on Best Practices for them to get a taste of their power.

In your Dockerfile write out the following:

```docker
FROM centos:latest
RUN yum install vim -y && mkdir /vim
WORKDIR /vim
ENTRYPOINT ["vim"]
```

Save the file and make sure it’s called Dockerfile.

Let’s talk about what the four lines above mean.

- FROM : creates a layer from the centos:latest Docker image
- RUN : builds your container by installing vim into it and creating a directory called /vim
- WORKDIR : informs the container where the working directory should be for it
- ENTRYPOINT : is the command that is run when the container starts, instead of
/bin/bash like how we did above

Now let’s build this locally. Run the following in the directory that the Dockerfile is and lets see this come together.

```bash
$ docker build .
```

The last line of the docker build output should be similar to this:

```bash
Successfully built eda2652aa25e
```

Note: You should have a different hash eda2652aa25e, so please keep that in mind.

Congratulations! You have built your first Dockerfile and customized docker container.
Let’s give it a run now. Go ahead and run the following command:

```bash
$ docker run -it eda2652aa25e
```

You should see vim start up! Remember, :q is how to quit it, and then you should see your command prompt again. You can run this as many times as you’d like and you’ll have a new instance of vim each time; but you can’t actually save anything or read anything because it’s a container right? Let's fix this in the next chapter.

## Persistence

We are going to add a bind mount to mount the local directory into the container. If you’d like to read more about mounts and other possibilities, we suggest starting at [https://docs.docker.com/storage/volumes/](https://docs.docker.com/storage/volumes/) – it’s one of the harder concepts but it’s worth your time.

On your command line, create a file called hello, then save the words *hello world* in it.

```bash
$ EDITOR hello
```

Note: Please your EDITOR of choice on your machine.

Now let’s mount the local directory you just created the hello file in into our container.

```bash
$ docker run -it -v ${PWD}:/vim eda2652aa25e
```

Inside of vim type :e hello. You should see hello world come up! As you can see, you opened the file that you created on the host machine, created a container with vim inside, mounted the directory and was able to open the file!
If you’d like you can type i and type something out, then type :wq when you’re done. The container should close out, and then you can type the following on your command line:

```bash
$ cat hello
hello world
TEC HandsOn is awesome
$
```

Note: Obviously "TEC HandsOn is awesome" is what we wrote and will be what you write inside your container.

Great you have finished this Docker tutorial.

## Additional resources

Besides our other tutorials there is a great Docker Essential course including very good videos explaining Docker. At the end there is a test and if you pass it you will get an badge from Acclaim: [https://cognitiveclass.ai/courses/docker-essentials/](https://cognitiveclass.ai/courses/docker-essentials/)

