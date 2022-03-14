# Docker Cheat Sheet

## Basics

### Identify and use a docker image

* `https://hub.docker.com` go here to look for images that may fit your needs
* `docker pull <image name>` pulls a docker image from a repository. start here
* `docker run <image name>` runs an instance of a container. _if image not found, will automatically do a `docker pull`_

## Dockerfile

### When to use a Dockerfile

{% hint style="info" %}
Use a Dockerfile to specify how your code gets packaged into a container&#x20;
{% endhint %}

A `Dockerfile` is useful when you want to run an application from a Docker container. Essentially, it's the file that provides the instructions to create the environment to run the app (i.e. `pip install -r requirements.txt`, commands you would normally run from the command prompt to run your script/ app, etc.). Once the Dockerfile is created, you can build your image, and then run the containe

### Basic steps for implementing a Dockerfile

**1. Create `Dockerfile`**

* Create file called `Dockerfile` in the directory of your project. _No file extension is needed._
* `FROM <baseImage:tag>`
  * Decide on a base image with any applicable tags you wish to use. This will be the first line of the Dockerfile. You can look on [dockerhub](https://hub.docker.com) to pick your base image.

**2. Build your container image using `docker build -t <imageName:tag> .`**

* Use `docker build --help` to find out more about what the `t` flag is used for if needed.
* Note the use of 'dot' `.` which assumes you are running the command from the same directory the `Dockerfile` is located in.
* `docker build` builds the container and stores as a locally runnable image&#x20;

**3. Run container using `docker run -<optional flags> <imageName>`**

* `docker run -d` or `docker run --detach` Run container in background and print container ID
* `docker run -p <#>:<#>` or `docker run --publish` Publish container port(s) to the host
* `docker run` is used to run the image&#x20;
