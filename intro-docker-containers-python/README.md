# Docker Containers

- [How do I create a Docker Image? ](#how-do-i-create-a-docker-image-)
  - [Prepare the code for Docker Container](#prepare-the-code-for-docker-container)
  - [Build the image](#build-the-image)
- [Docker Cheat-Sheet](#docker-cheat-sheet)
- [Next Steps](#next-steps)

## How do I create a Docker Image?

### Prepare the code for Docker Container

The application for which we'll build the container is a simple, “Hello World” app that uses Flask, a small HTTP server for Python apps.

Imagine you’re trying to deploy the following Python code, contained in index.py.

*index.py*

~~~python
import os

from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello World!"
if __name__ == "__main__":
    #app.run(host="0.0.0.0", port=int("5000"), debug=True)
	app.run(debug=True, host='0.0.0.0', port=int(os.environ.get('PORT', 8080)))
~~~

To do so, create a text file called Dockerfile in your application’s root and paste in the following code.

*Dockerfile*

~~~dockerfile
FROM python:alpine3.7
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
RUN chmod 444 index.py
RUN chmod 444 requirements.txt
 
# Service must listen to $PORT environment variable.
# This default value facilitates local development.
ENV PORT 8080
CMD python ./index.py
~~~

Note that **FROM** directive is pointing to **python:alpine3.7**. This is telling Docker what base image to use for the container, and implicitly selecting the Python version to use, which in this case is 3.7. Docker Hub has base images for almost all supported versions of Python. This example is using Python installed on Alpine Linux, a minimalist Linux distro, which helps keep the images for Docker small. Prefer Alpine unless there’s a compelling reason to use another base image such as Debian Jessie.

Also note is the **RUN** directive that is calling PyPi (**pip**) and pointing to the requirements.txt file. This file contains a list of the dependencies that the application needs to run. Because Flask is a dependency, it is included as such in the **requirements.txt** with a simple reference. You can also select version libraries if you need specific versions with requirements.txt. The file should also be in the root of the application.

*requirements.txt*

~~~
flask
~~~

The remaining directives in the **Dockerfile** are pretty straightforward. The **CMD** directive tells the container what to execute to start the application. In this case, it is telling Python to run **index.py**. The **COPY** directive simply moves the application into the container image, **WORKDIR** sets the working directory.

To make new software easier to run, **ENV** can be used to update for example the **PORT** environment variable for the software the container installs. The application reads the port from the environment variables `port=int(os.environ.get('PORT', 8080))`.

*Only for Windows users:*
The **chmod** commands are needed to avoid security warnings for Docker on Windows. The problem is that the Dockerfile COPY statements add execution permission to files. The chmod commands change the file permissions back to read-only. 

The needed code can be also taken from github: /helloworld-cloud/tree/master/intro-docker-containers/helloworldinpython.


### Build the image

To build the image, run Docker build from a command line or terminal that is in the root directory of the application.

~~~
docker build --tag my-python-app .
~~~

This will “tag” the image my-python-app and build it. After it is built, you can run the image as a container.

~~~
docker run --name python-app -p 8080:8080 my-python-app
~~~

This starts the application as a container. The **–name** parameter names the container and the **-p** parameter maps the host’s port 5000 to the containers port of 5000. Lastly, the my-python-app refers to the image to run. After it starts, you should be able to browse to the container. Depending on how you are running Docker depends on what the IP address of the application will be. Docker for Windows and Docker for Mac will be able to use 127.0.0.1. For other instances, it will be the host IP of a VM or physical machine you are running Docker on.

You should be able to open following URL and see your application running:

~~~
http://127.0.0.1:8080/
~~~


## Docker Cheat-Sheet

Find out the Docker verion

~~~
docker --version
~~~

Get an image from the Docker Hub Repository - https://hub.docker.com/search?q=&type=image

~~~
docker pull ubuntu
~~~

Create a container from an image:

~~~
docker run <options> <image_name>

Options:
--rm remove container automatically after it exits
--it connect the container to terminal
--name <container-name> name the container
-p 5000:80 expose port 5000 externally and map to port 80
/bin/sh the command to run inside the container
~~~

Access a running container:

~~~
docker exec -it <CONTAINER-ID> bash
~~~


Stop a running container

~~~
docker stop <CONTAINER-ID>
~~~

Kill the container by stopping its execution immediately. 
The difference between ‘docker kill’ and ‘docker stop’ is that ‘docker stop’ gives the container time to shutdown gracefully, in situations when it is taking too much time for getting the container to stop, one can opt to kill it

~~~
docker kill <CONTAINER-ID>
~~~

Create a new image of an edited container on the local system

~~~
docker commit <conatainer id> <username/imagename>
~~~

Push an image to the docker hub repository

~~~
docker push <username/image name>
~~~

This command lists all the locally stored docker images

~~~
docker images
~~~

Delete a stopped container

~~~
docker rm <container id>
~~~

Delete an image from local storage

~~~
docker rmi <image-id>
~~~

Build an image from a specified docker file

~~~
docker build <path to docker file>
~~~


## Next Steps
Now that you can create images, you should try to deploy containers on the different clouds:

* [Google Cloud Platform - GCP](../cloud-gcp)
* [Microsoft Azure](../cloud-ms-azure)
* [AWS](../cloud-aws)
* [IBM Cloud](../cloud-ibm-cloud)
