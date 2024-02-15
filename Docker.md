# Table of contents

Docker

Installation Docker on Linux:-

Docker Basics:-

Docker daemon and client:-

Docker Client (You):-

The layers concept:-

Docker Volume:-

Data Persistence:-

Shared Storage:-

Container-to-Container Communication:-

Syntax for Using Volumes:-

Docker networking:-

Custom Bridge Networks:-

Host Network:-

Overlay Network:-

Service Discovery and DNS:-

Network Inspect and Troubleshooting:-

Docker networking (DNS Enable):-

Docker Registry:-

Registry Server:-

Docker Repository:-












# Docker
Docker is like a superhero for software. It helps developers package their applications, along with all the stuff they need to run, into something called a "container." This container includes the code, libraries, and dependencies, making sure the software works the same way no matter where it's run.
Now, the cool part is that these containers can run on any computer that has Docker installed. It's like having a portable, consistent environment for your software. So, whether your app is on your laptop during development, or on a big server in the cloud, Docker ensures it behaves the same way.
Think of Docker as a shipping container for your software—everything neatly packed, easily movable, and ready to work anywhere. It makes developing, testing, and deploying applications much smoother and more reliable.

* 1: Containerization:
Containers: Containers are like magic boxes for software. Imagine          you have a special box that holds everything your software needs to run: the code, libraries, and other necessary stuff. This box is a container.
Now, these containers are super cool because they can run the same way on any computer that has the right "magic" installed. It's like having a portable home for your software that you can easily move around.
Features of container -It is lighter weight,flexible,interchangeable etc.


* 2: Docker Images:
Docker image is like a snapshot or template of a software application, containing all the necessary files, libraries, and dependencies needed to run the application smoothly. It's a lightweight, standalone, and executable package that encapsulates everything needed to run a piece of software, including the code, runtime, system tools, system libraries, and settings.

Think of it as a recipe for creating a specific dish. Just like a recipe lists all the ingredients and instructions needed to cook a meal, a Docker image contains all the components and instructions needed to run an application. This makes it easy to share and deploy software across different environments, as the image ensures consistency and reproducibility of the application's runtime environment.

* 3:Dockerfile: 
Docker image is like a packed box that contains all the necessary files, tools, and settings to run a piece of software. It's self-contained, portable, and can be easily moved and deployed onto different computer systems. When you run a Docker image, it sets up a virtual environment with everything the software needs to run correctly. This makes it easier for developers to package, distribute, and run their applications consistently across different environments.

##  Installation Docker on Linux
## Prerequisites:
```Distributor ID:	Ubuntu
Description:	Ubuntu 22.04.3 LTS
Release:	22.04
Codename:	jammy
``````

### Step 1: Install Docker using the following command:

 ```
 sudo apt install docker.io
 ```
To check version:
```
Sudo docker --version
```
Output:  
Docker version 24.0.7, build afdd53b 
To check the status of docker we have:  
```
sudo systemctl status docker  
```
●  docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2024-02-15 09:54:37 IST; 44min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 2300 (dockerd)
      Tasks: 52
     Memory: 105.1M
     CGroup: /system.slice/docker.service
             └─2300 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock


If your docker status is not active:
```
sudo systemctl enable --now docker
```
## Docker Basics    

To pull image from dockerhub use the following command:-  
```
sudo docker pull hello-world  
```
Output:   
Using default tag: latest
latest: Pulling from library/hello-world
Digest: sha256:d000bc569937abbe195e20322a0bde6b2922d805332fd6d8a68b19f524b7d21d
Status: Image is up to date for hello-world:latest
docker.io/library/hello-world:latest


**To check the list of images:-**
```
sudo docker image ls
```
**Output:**

     REPOSITORY        TAG       IMAGE ID       CREATED        SIZE
ubuntu            20.04     18ca3f4297e7   3 weeks ago    72.8MB
ubuntu            latest    174c8c134b2a   2 months ago   77.9MB
nginx             latest    a8758716bb6a   3 months ago   187MB
ubuntu            18.04     f9a80a55f492   8 months ago   63.2MB
hello-world       latest    d2c94e258dcb   9 months ago   13.3kB
docker/whalesay   latest    6b362a9f73eb   8 years ago    247MB


To run image use this following command:
```
sudo docker run hello-world
```
Output:  
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

 
## Docker daemon and client: 
The Docker daemon and client are like a team that helps you work with containers.:
Analogy: Imagine the Docker daemon as a diligent backstage assistant.
Role: The daemon handles the grunt work, overseeing containers, images, and all Docker-related tasks on your computer.
Job: Much like a reliable handyman, it's responsible for constructing, initiating, and halting containers. Essentially, it's your dependable helper, always available to execute tasks efficiently in the background.

## Docker Client (You):
Analogy: Picture the Docker client as your approachable manager or supervisor.
Role: The client serves as your communication tool, facilitating interaction with the daemon.
Job: As the client, you issue directives (e.g., 'build this container' or 'run that image') to the daemon. Through this interface, you communicate your requirements, and the client ensures tasks are carried out by engaging with the daemon. In simpler terms, you're the one giving orders, and the client acts as your messenger to get things done.

## The layers concept.
when you create a Docker image using a Dockerfile, each command you specify in the Dockerfile generates a layer in the resulting image. These layers are fundamental for several reasons:

Optimizing Image Size: Docker layers enable efficient use of storage space by reusing common layers across multiple images. This reduces the overall size of images, making them more manageable and easier to distribute.

Improving Build Speed: Because Docker caches intermediate layers, subsequent builds that reuse unchanged layers can be significantly faster. This caching mechanism speeds up the development and deployment process, particularly for iterative development workflows.

Managing Image Updates: Docker layers facilitate incremental updates to images. When you modify a Dockerfile and rebuild an image, only the affected layers need to be rebuilt, while unchanged layers can be reused. This enables rapid and efficient updates to containerized applications.
```
mkdir kemo
```
```
deepak@deepak:~$ cd kemo
deepak@deepak:~/kemo$ touch Dockerfile
deepak@deepak:~/kemo$ vi Dockerfile
FROM Ubuntu:23.04
```



```
deepak@deepak:~/kemo$ sudo docker image build -t myoperation:01 .
```
```
[+] Building 0.1s (5/5) FINISHED                                                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                  0.0s
 => => transferring dockerfile: 95B                                                                                                                                                                   0.0s
 => [internal] load .dockerignore                                                                                                                                                                     0.0s
 => => transferring context: 2B                                                                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:20.04                                                                                                                                       0.0s
 => [1/1] FROM docker.io/library/ubuntu:20.04                                                                                                                                                         0.0s
 => exporting to image                                                                                                                                                                                0.0s
 => => exporting layers                                                                                                                                                                               0.0s
 => => writing image sha256:09d9bda708dc6a56f36d0e8841c194e04c290646659ecbf409e52b8032cacd7d                                                                                                          0.0s
 => => naming to docker.io/library/myoperation:01                                                                                                                                                     0.0s
deepak@deepak:~/kemo$ 


deepak@deepak:~/kemo$ sudo docker image ls
REPOSITORY        TAG       IMAGE ID       CREATED        SIZE
myoperation       01        09d9bda708dc   3 weeks ago    72.8MB
ubuntu            20.04     18ca3f4297e7   3 weeks ago    72.8MB
ubuntu            latest    174c8c134b2a   2 months ago   77.9MB
nginx             latest    a8758716bb6a   3 months ago   187MB
ubuntu            18.04     f9a80a55f492   8 months ago   63.2MB
hello-world       latest    d2c94e258dcb   9 months ago   13.3kB
docker/whalesay   latest    6b362a9f73eb   8 years ago    247MB


```
deepak@deepak:~/kemo$ sudo docker image build -t myoperation:02 .
```

Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM ubuntu:23.04
 ---> 09d9bda708dc
Step 2/2 : RUN apt-get update && apt-get install -y tree
 ---> Running in 10090c78c832
[+] Building 31.5s (9/9) FINISHED                                                                                                                                                           docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                  0.0s
 => => transferring dockerfile: 222B                                                                                                                                                                  0.0s
 => [internal] load .dockerignore                                                                                                                                                                     0.0s
 => => transferring context: 2B                                                                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:23.04                                                                                                                                       5.5s
 => [stage-1 1/5] FROM docker.io/library/ubuntu:23.04@sha256:5a828e28de105c3d7821c4442f0f5d1c52dc16acf4999d5f31a3bc0f03f06edd                                                                         5.7s
 => => resolve docker.io/library/ubuntu:23.04@sha256:5a828e28de105c3d7821c4442f0f5d1c52dc16acf4999d5f31a3bc0f03f06edd                                                                                 0.0s
 => => sha256:5a828e28de105c3d7821c4442f0f5d1c52dc16acf4999d5f31a3bc0f03f06edd 1.13kB / 1.13kB                                                                                                        0.0s
 => => sha256:ea1285dffce8a938ef356908d1be741da594310c8dced79b870d66808cb12b0f 424B / 424B                                                                                                            0.0s
 => => sha256:f4cdeba72b994748f5eb1f525a70a9cc553b66037ec37e23645fbf3f0f5c160d 2.30kB / 2.30kB                                                                                                        0.0s
 => => sha256:6360b371721185fefbbad6763ab745900f1b2f7714570234473232dd575fc07f 26.89MB / 26.89MB                                                                                                      4.8s
 => => extracting sha256:6360b371721185fefbbad6763ab745900f1b2f7714570234473232dd575fc07f                                                                                                             0.7s
 => [stage-1 2/5] RUN apt-get update && apt-get install -y tree                                                                                                                                      18.5s
 => [stage-1 3/5] RUN pwd>/tmp/1stpwd.txt                                                                                                                                                             0.5s
 => [stage-1 4/5] RUN cd /tmp/                                                                                                                                                                        0.4s 
 => [stage-1 5/5] RUN pwd>/tmp/2ndpwd.txt                                                                                                                                                             0.4s 
 => exporting to image                                                                                                                                                                                0.3s 
 => => exporting layers                                                                                                                                                                               0.3s 
 => => writing image sha256:afd5915f3c516e41b7122470a22c10edb8939e7cff0ce76a8b5233c291dfe05f                                                                                                          0.0s 
 => => naming to docker.io/library/myoperation:02                                                                                                                                                     0.0s
deepak@deepak:~/kemo$ 

deepak@deepak:~/kemo$ sudo docker image ls
REPOSITORY        TAG       IMAGE ID       CREATED         SIZE
myoperation       02        afd5915f3c51   7 minutes ago   112MB
ubuntu            20.04     18ca3f4297e7   3 weeks ago     72.8MB
myoperation       01        09d9bda708dc   3 weeks ago     72.8MB
ubuntu            latest    174c8c134b2a   2 months ago    77.9MB
nginx             latest    a8758716bb6a   3 months ago    187MB
ubuntu            18.04     f9a80a55f492   8 months ago    63.2MB
hello-world       latest    d2c94e258dcb   9 months ago    13.3kB
docker/whalesay   latest    6b362a9f73eb   8 years ago     247MB

deepak@deepak:~/kemo$ vi dockerfile
RUN pwd>/tmp/1stpwd.txt
RUN cd /tmp/
RUN pwd>/tmp/2ndpwd.txt
deepak@deepak:~/kemo$ sudo docker image build -t myoperation:3.1 .
Sending build context to Docker daemon  2.048kB
Step 1/5 : FROM ubuntu:23.04
 ---> afd5915f3c51
Step 2/5 : RUN apt-get update && apt-get install -y tree
 ---> Using cache
 ---> afd5915f3c51
Step 3/5 : RUN touch /tmp/1.txt
 ---> Running in d7653aefe442
Removing intermediate container d7653aefe442
 ---> 06eba0e8b762
Step 4/5 : RUN touch /tmp/2.txt
 ---> Running in dv5c1c313a79
Removing intermediate container dv5c1c313a79
 ---> 9de01433b498
Step 5/5 : RUN touch /tmp/3.txt
 ---> Running in 74b375c7ba8f
Removing intermediate container 74b375c7ba8f
 ---> 9e229711ab23
Successfully built e229711ab23
Successfully tagged myoperation:3.1

[+] Building 2.7s (12/12) FINISHED                                                                                                                                                          docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                  0.0s
 => => transferring dockerfile: 292B                                                                                                                                                                  0.0s
 => [internal] load .dockerignore                                                                                                                                                                     0.0s
 => => transferring context: 2B                                                                                                                                                                       0.0s
 => [internal] load metadata for docker.io/library/ubuntu:23.04                                                                                                                                       1.1s
 => [stage-1 1/8] FROM docker.io/library/ubuntu:23.04@sha256:5a828e28de105c3d7821c4442f0f5d1c52dc16acf4999d5f31a3bc0f03f06edd                                                                         0.0s
 => CACHED [stage-1 2/8] RUN apt-get update && apt-get install -y tree                                                                                                                                0.0s
 => CACHED [stage-1 3/8] RUN pwd>/tmp/1stpwd.txt                                                                                                                                                      0.0s
 => CACHED [stage-1 4/8] RUN cd /tmp/                                                                                                                                                                 0.0s
 => CACHED [stage-1 5/8] RUN pwd>/tmp/2ndpwd.txt                                                                                                                                                      0.0s
 => [stage-1 6/8] RUN touch /tmp/1.txt                                                                                                                                                                0.3s
 => [stage-1 7/8] RUN touch /tmp/2.txt                                                                                                                                                                0.6s
 => [stage-1 8/8] RUN touch /tmp/3.txt                                                                                                                                                                0.5s
 => exporting to image                                                                                                                                                                                0.1s
 => => exporting layers                                                                                                                                                                               0.1s
 => => writing image sha256:a3eb20e4f0b78d12b24d9508ba55af43c51891ca8fc29f378a10fae8098a4e32                                                                                                          0.0s
 => => naming to docker.io/library/myoperation:3.1                                                                                                                                                    0.0s
deepak@deepak:~/kemo$ 


```
deepak@deepak:~/kemo$ cat dockerfile
```

FROM ubuntu:20.04
FROM ubuntu:23.04
RUN apt-get update && apt-get install -y tree
RUN pwd>/tmp/1stpwd.txt
RUN cd /tmp/
RUN pwd>/tmp/2ndpwd.txt
RUN touch /tmp/1.txt   
RUN touch /tmp/2.txt  
RUN touch /tmp/3.txt  

```
deepak@deepak:~/kemo$ sudo docker image ls |wc
```
 10      69     644




###All commands used in layered concept

```FROM ubuntu:23.04
LABEL name="deepak"
LABEL email="cu.16bcs2823@gmail.com"
ENV NAME saket
ENV PASS password
RUN pwd>/tmp/1stpwd.txt
RUN cd /tmp/
RUN pwd>/tmp/2ndpwd.txt
WORKDIR /tmp
RUN pwd>/tmp/3rdpwd.txt
RUN apt-get update && apt-get install -y openssh-server && apt-get update && apt-get install -y python
RUN useradd -d /home/deepak1 -g root -G sudo -m -p $(echo "$PASS" | openssl passwd -1 -stdin) $NAME
RUN whoami > /tmp/1stwhoami.txt
USER $NAME
RUN whoami > /tmp/2ndwhoami.txt
RUN mkdir -p /tmp/project
COPY dockerfile /tmp/project/
CMD ["sh"]
```

## Docker Volume:
Docker volumes offer a method for storing and maintaining data within Docker containers. They serve as a means to persist data beyond the lifecycle of containers, enabling storage that can be shared between a container and the host system or among multiple containers. Here are some key aspects of Docker volumes:

## Data Persistence: 
Docker volumes ensure that data persists even if containers are stopped, removed, or replaced. This allows essential data, such as application configurations, databases, or user uploads, to remain intact across container instances.

## Data Sharing: 
Volumes enable seamless sharing of data between containers or between containers and the host system. This facilitates collaboration and communication between different components of an application stack, allowing them to access and manipulate shared data.

## Data Management:
Docker volumes provide a centralized mechanism for managing data storage within the Docker ecosystem. They offer features such as backup, restoration, and versioning, allowing administrators to efficiently handle data-related tasks.

## Performance Optimization: 
Volumes can improve performance by separating data storage from container filesystems. This reduces the overhead associated with container startup and runtime, resulting in faster operation and improved resource utilization.

## Flexibility: 
Docker volumes support various types of storage backends, including local disk storage, networked storage, and cloud-based storage solutions. This flexibility allows users to choose the most suitable storage option based on their specific requirements and infrastructure setup.

## Container-to-Container Communication:
Volumes enable communication and data sharing between different containers. Multiple containers can mount the same volume, allowing them to access and modify shared data.

## Syntax for Using Volumes:
Volumes can be specified in the Docker run command or in a Docker Compose file using the -v option. 
Code of Docker Volume my sql data persist in docker container
```
sudo docker volume create my_password_volume
```
Creates a Docker volume named my_password_volume. This volume can be used to persistently store data within Docker containers.
[sudo] password for deepak:

Output:  
my_password_volume


```
sudo docker volume ls
[sudo] password for deepak:
```
This is used to list all Docker volumes present on your system. 
OUTPUT:
DRIVER    VOLUME NAME
local     my_password_volume
```
sudo docker image ls 
```
REPOSITORY        TAG       IMAGE ID       CREATED        SIZE
myoperation       3.1       a3eb20e4f0b7   3 hours ago    112MB
myoperation       02        afd5915f3c51   3 hours ago    112MB
ubuntu            20.04     18ca3f4297e7   3 weeks ago    72.8MB
myoperation       01        09d9bda708dc   3 weeks ago    72.8MB
ubuntu            latest    174c8c134b2a   2 months ago   77.9MB
nginx             latest    a8758716bb6a   3 months ago   187MB
ubuntu            18.04     f9a80a55f492   8 months ago   63.2MB
hello-world       latest    d2c94e258dcb   9 months ago   13.3kB
docker/whalesay   latest    6b362a9f73eb   8 years ago    247MB

```
```
sudo docker image inspect nginx
```
This is used to inspect the details of a Docker image named "nginx."   
[sudo] password for deepak:
```
Output:
[
    {
        "Id": "sha256:a8758716bb6aa4d90071160d27028fe4eaee7ce8166221a97d30440c8eac2be6",
        "RepoTags": [
            "nginx:latest"
        ],
        "RepoDigests": [
            "nginx@sha256:4c0fdaa8b6341bfdeca5f18f7837462c80cff90527ee35ef185571e1c327beac"
        ],
        "Parent": "",
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2023-10-24T22:44:45Z",
        "Container": "",
        "ContainerConfig": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": null,
            "Cmd": null,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "DockerVersion": "",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.25.3",
                "NJS_VERSION=0.8.2",
                "PKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "ArgsEscaped": true,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 186728317,
        "VirtualSize": 186728317,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/b36101af8c5d0e8849d017bc6259defd1f2b69d6e9f5fa3887ef7cdea525e41d/diff:/var/lib/docker/overlay2/f124f5479b765fb844cfbda608f69fac5cfb7939d826f438441d4ddf9be84efa/diff:/var/lib/docker/overlay2/99fdc1dec78da8587b4cc72593f2d34c73c7a8704d2bfe713fe8bb743a37cc14/diff:/var/lib/docker/overlay2/b85cd8ceb9f7c69ed6d3edb261205f1bb933a91e587f3eb42b90568a5a0d7ae2/diff:/var/lib/docker/overlay2/0a11e40dc43d7ae0e98223db65defc3a854103712473c3bf8f868b8398be33bd/diff:/var/lib/docker/overlay2/8bda9bc5f7db5db1f32d6400e7e1dbe931c1bf647a813b7e2109cf431a54ee77/diff",
                "MergedDir": "/var/lib/docker/overlay2/329ed97de5b364bf29a4d9f3ac55aec1f37eae232c37e63f8299868e20cf9ba7/merged",
                "UpperDir": "/var/lib/docker/overlay2/329ed97de5b364bf29a4d9f3ac55aec1f37eae232c37e63f8299868e20cf9ba7/diff",
                "WorkDir": "/var/lib/docker/overlay2/329ed97de5b364bf29a4d9f3ac55aec1f37eae232c37e63f8299868e20cf9ba7/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:571ade696b261f0ff46e3cdac4635afc009c4ed3429950cb95cd7e5f70ba0a07",
                "sha256:b6c2a8d6f0ac89ef77e161532f3d9d0dc5dfe0a5f20042e0afc0ad14288405eb",
                "sha256:b61d4b2cd2daf06047984c5876a35338c2beb5ae3f6bef479d25f05772a6a482",
                "sha256:eddcd06e5ef9b91677526f6c55fa01a7d6963c435d5cf2bfb488d91aaa72d4a8",
                "sha256:b4ad478450363f0a8020bb5552641fe6077e78fca48da4d77a979724a3ad2a72",
                "sha256:fbcc9bc44d3e165e7e4f56fb189a05ea5c562a733985ec00d5e3fad309eb63cc",
                "sha256:009507b8560964795eab5126f6363cb2b7403596adf370c9e95d4648c43e771f"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]

```
```
sudo docker container run -d --name nginx nginx:latest
NGINX_ALLOW_EMPTY_PASSWORD=true nginx
```
```
sudo docker volume inspect my_password_volume
 
```
```
05f30291c17c3431c60e184e79660d380f5fec682cd29d8eff95ce449f3ba503

```
This is used to inspect the details of a specific Docker volume with the identifier "05f30291c17c3431c60e184e79660d380f5fec682cd29d8eff95ce449f3ba503" 

```
Output
[
    {
        "CreatedAt": "2024-01-18T16:19:06+05:30",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/05f30291c17c3431c60e184e79660d380f5fec682cd29d8eff95ce449f3ba503/_data",
        "Name": "05f30291c17c3431c60e184e79660d380f5fec682cd29d8eff95ce449f3ba503",
        "Options": null,
        "Scope": "local"
    }
]

```
```
ls -lrth |grep docker
-rw-rw-r-- 1 deepak deepak  22K Jan 16 19:03 get-docker.sh
```

This is used to list files in the current directory, sort them by modification time in reverse order (oldest first), and then filter the output to show only those lines containing the word "docker."
```
sudo chown deepak:root get-docker.sh

```
This is used to change the ownership of the "docker" directory to the user "deepak" and the group "root."
```
cd  /var/lib/docker/volumes/05f30291c17c3431c60e184e79660d380f5fec682cd29d8eff95ce449f3ba503/_data
```
This is used to change the current working directory to the location where the contents of a Docker volume with the identifier "05f30291c17c3431c60e184e79660d380f5fec682cd29d8eff95ce449f3ba503" are stored on the host machine.

```
sudo docker container ls
```
```
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
05f30291c17c   nginx:latest   "/docker-entrypoint.…"   33 minutes ago   Up 33 minutes   80/tcp    nginx

```



## Docker networking:
Docker networking involves the setups and settings that allow Docker containers to communicate with one another and with external networks. Docker offers various networking options to facilitate smooth interaction between containers.

The default bridge network is the network that Docker containers are connected to when no specific network is specified during container creation.

Containers within the same bridge network can communicate with each other using either their container names or IP addresses. This means that if you have multiple containers running on the same Docker host and connected to the default bridge network, they can easily exchange data and interact with each other using simple addressing methods.

For instance, if you have two containers named "container1" and "container2" running on the same default bridge network, "container1" can communicate with "container2" simply by using its name, like this: ping container2. Alternatively, they can communicate using each other's IP addresses within the same network.

### Custom Bridge Networks:
Docker enables users to establish customized bridge networks through the 'docker network create' command. These custom bridge networks provide a way for containers to communicate with each other, enhancing flexibility and control over networking configurations.
Containers within the same custom bridge network can communicate with each other using container names or service discovery.

### Host Network:
Containers can use the host network mode, sharing the network namespace with the Docker host.
This mode provides maximum network performance but may expose ports directly on the host.

### Overlay Network:
Docker Swarm uses overlay networks for multi-host communication in a cluster.
Containers in the overlay network can communicate seamlessly across multiple nodes.

### Service Discovery and DNS:
Docker includes built-in DNS resolution for container names within the same network.
Containers can discover and communicate with each other using container names.

### Network Inspect and Troubleshooting:
The docker network inspect command allows you to view details of a network, including connected containers.
Troubleshooting commands help diagnose and resolve network-related issues.
```
sudo docker network ls
```
```
Output:
NETWORK ID     NAME      DRIVER    SCOPE
92c71048ffd1   bridge    bridge    local
e3aed1fa8996   host      host      local
361dbf23c474   none      null      local

```
```
sudo docker container run -itd nginx
```
This command is using Docker to run a detached (in the background) instance of the official Nginx (web server) container in interactive mode.
``` 
fdfdb1bb5d91a532ceae177ead7d6071e3fe3859f2fe6226b1b13acb0e36368f
```
```
sudo docker container ls
```
```
Output:
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS     NAMES
d26805aaca63   nginx          "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    exciting_ptolemy
05f30291c17c   nginx:latest   "/docker-entrypoint.…"   50 minutes ago       Up 3 minutes        80/tcp    nginx

```
```
sudo docker network inspect bridge
```
The command sudo docker network inspect bridge is used to retrieve information about the default bridge network in Docker. 

Output:
```
[
    {
        "Name": "bridge",
        "Id": "92c71048ffd1335e6bfdaf0306d6d91229d8b93d721d1c04850b5a2aa861549c",
        "Created": "2024-02-15T10:48:33.181350049+05:30",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "05f30291c17c3431c60e184e79660d380f5fec682cd29d8eff95ce449f3ba503": {
                "Name": "nginx",
                "EndpointID": "d818741ca6686b1c86a30470f231ea0d5f23c7eec97ca682d39c1d22d527b640",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            },
            "d26805aaca634b5e905ad673b107d0118a433379420bbba3495d4a6bd4ba0e26": {
                "Name": "exciting_ptolemy",
                "EndpointID": "0e9e5460ff361b0848753832efa0cde561de1b5d850e18a4fcbc69ff984963e1",
                "MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            },
            "fdfdb1bb5d91a532ceae177ead7d6071e3fe3859f2fe6226b1b13acb0e36368f": {
                "Name": "awesome_meninsky",
                "EndpointID": "20cbe8e373946aca91b1074a1e7a6bdfcbdfb8266cec1d5700f027f51f30d674",
                "MacAddress": "02:42:ac:11:00:04",
                "IPv4Address": "172.17.0.4/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]

```
```
sudo docker container run -it ubuntu
```
This command is using Docker to run an interactive (in the foreground) instance of the official Ubuntu container.  

```
Output:
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
5e8117c0bd28: Pull complete 
Digest: sha256:8eab65df33a6de2844c9aefd19efe8ddb87b7df5e9185a4ab73af936225685bb
Status: Downloaded newer image for ubuntu:latest

```
```
apt-get update && apt-get install iputils-ping
```
This is used to update the package list on a Debian-based Linux system and then install the iputils-ping package.

Output:
```
Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]                                
Get:2 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]                                          
Get:3 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [1070 kB]
Get:4 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [1456 kB]
Get:5 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [1784 kB]
Get:6 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]        
Get:7 http://security.ubuntu.com/ubuntu jammy-security/multiverse amd64 Packages [44.6 kB]
Get:8 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [109 kB]       
Get:9 http://archive.ubuntu.com/ubuntu jammy/restricted amd64 Packages [164 kB]
Get:10 http://archive.ubuntu.com/ubuntu jammy/multiverse amd64 Packages [266 kB]
Get:11 http://archive.ubuntu.com/ubuntu jammy/main amd64 Packages [1792 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy/universe amd64 Packages [17.5 MB]
Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [1822 kB]                                                                                                                 
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [50.4 kB]                                                                                                                 
Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1343 kB]                                                                                                                   
Get:16 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1735 kB]                                                                                                                       
Get:17 http://archive.ubuntu.com/ubuntu jammy-backports/main amd64 Packages [50.4 kB]                                                                                                                     
Get:18 http://archive.ubuntu.com/ubuntu jammy-backports/universe amd64 Packages [28.1 kB]                                                                                                                 
Fetched 29.7 MB in 11s (2699 kB/s)                                                                                                                                                                        
Reading package lists... Done
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libcap2-bin libpam-cap
The following NEW packages will be installed:
  iputils-ping libcap2-bin libpam-cap
0 upgraded, 3 newly installed, 0 to remove and 12 not upgraded.
Need to get 76.8 kB of archives.
After this operation, 280 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcap2-bin amd64 1:2.44-1ubuntu0.22.04.1 [26.0 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 iputils-ping amd64 3:20211215-1 [42.9 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpam-cap amd64 1:2.44-1ubuntu0.22.04.1 [7928 B]
Fetched 76.8 kB in 1s (61.2 kB/s)  
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libcap2-bin.
(Reading database ... 4393 files and directories currently installed.)
Preparing to unpack .../libcap2-bin_1%3a2.44-1ubuntu0.22.04.1_amd64.deb ...
Unpacking libcap2-bin (1:2.44-1ubuntu0.22.04.1) ...
Selecting previously unselected package iputils-ping.
Preparing to unpack .../iputils-ping_3%3a20211215-1_amd64.deb ...
Unpacking iputils-ping (3:20211215-1) ...
Selecting previously unselected package libpam-cap:amd64.
Preparing to unpack .../libpam-cap_1%3a2.44-1ubuntu0.22.04.1_amd64.deb ...
Unpacking libpam-cap:amd64 (1:2.44-1ubuntu0.22.04.1) ...
Setting up libcap2-bin (1:2.44-1ubuntu0.22.04.1) ...
Setting up libpam-cap:amd64 (1:2.44-1ubuntu0.22.04.1) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 78.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.34.0 /usr/local/share/perl/5.34.0 /usr/lib/x86_64-linux-gnu/perl5/5.34 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.34 /usr/share/perl/5.34 /usr/local/lib/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up iputils-ping (3:20211215-1) ...
```
```
ping 8.8.8.8 
```

The ping command is commonly used to test network connectivity and measure the round-trip time for packets to travel from the source to the destination and back.
```
Output:
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=111 time=87.0 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=111 time=46.0 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=111 time=46.0 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=111 time=44.2 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=111 time=43.0 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=111 time=45.9 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=111 time=39.5 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=111 time=36.5 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=111 time=60.9 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=111 time=58.0 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=111 time=61.7 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=111 time=49.5 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=111 time=46.9 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=111 time=50.6 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=111 time=48.0 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=111 time=35.9 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=111 time=40.8 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=111 time=18.1 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=111 time=216 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=111 time=35.0 ms
64 bytes from 8.8.8.8: icmp_seq=21 ttl=111 time=260 ms
64 bytes from 8.8.8.8: icmp_seq=22 ttl=111 time=282 ms
64 bytes from 8.8.8.8: icmp_seq=23 ttl=111 time=57.0 ms
64 bytes from 8.8.8.8: icmp_seq=24 ttl=111 time=38.5 ms
64 bytes from 8.8.8.8: icmp_seq=25 ttl=111 time=47.0 ms
64 bytes from 8.8.8.8: icmp_seq=26 ttl=111 time=45.2 ms
64 bytes from 8.8.8.8: icmp_seq=27 ttl=111 time=42.8 ms
64 bytes from 8.8.8.8: icmp_seq=28 ttl=111 time=44.2 ms
64 bytes from 8.8.8.8: icmp_seq=29 ttl=111 time=44.9 ms
64 bytes from 8.8.8.8: icmp_seq=30 ttl=111 time=38.0 ms
64 bytes from 8.8.8.8: icmp_seq=31 ttl=111 time=56.5 ms
64 bytes from 8.8.8.8: icmp_seq=32 ttl=111 time=34.6 ms
64 bytes from 8.8.8.8: icmp_seq=33 ttl=111 time=52.6 ms
64 bytes from 8.8.8.8: icmp_seq=34 ttl=111 time=50.0 ms
64 bytes from 8.8.8.8: icmp_seq=35 ttl=111 time=69.2 ms
64 bytes from 8.8.8.8: icmp_seq=36 ttl=111 time=47.6 ms
64 bytes from 8.8.8.8: icmp_seq=37 ttl=111 time=45.0 ms
64 bytes from 8.8.8.8: icmp_seq=38 ttl=111 time=47.7 ms
64 bytes from 8.8.8.8: icmp_seq=39 ttl=111 time=40.8 ms
64 bytes from 8.8.8.8: icmp_seq=40 ttl=111 time=23.5 ms
64 bytes from 8.8.8.8: icmp_seq=41 ttl=111 time=55.7 ms
64 bytes from 8.8.8.8: icmp_seq=42 ttl=111 time=33.6 ms
64 bytes from 8.8.8.8: icmp_seq=43 ttl=111 time=51.8 ms
64 bytes from 8.8.8.8: icmp_seq=45 ttl=111 time=40.9 ms
64 bytes from 8.8.8.8: icmp_seq=46 ttl=111 time=38.1 ms
64 bytes from 8.8.8.8: icmp_seq=47 ttl=111 time=56.3 ms
64 bytes from 8.8.8.8: icmp_seq=48 ttl=111 time=34.5 ms
64 bytes from 8.8.8.8: icmp_seq=49 ttl=111 time=55.9 ms
64 bytes from 8.8.8.8: icmp_seq=50 ttl=111 time=50.8 ms
64 bytes from 8.8.8.8: icmp_seq=51 ttl=111 time=55.0 ms
64 bytes from 8.8.8.8: icmp_seq=52 ttl=111 time=48.5 ms
64 bytes from 8.8.8.8: icmp_seq=53 ttl=111 time=80.3 ms
64 bytes from 8.8.8.8: icmp_seq=54 ttl=111 time=47.9 ms
64 bytes from 8.8.8.8: icmp_seq=55 ttl=111 time=42.1 ms
64 bytes from 8.8.8.8: icmp_seq=56 ttl=111 time=59.9 ms
64 bytes from 8.8.8.8: icmp_seq=57 ttl=111 time=49.1 ms
64 bytes from 8.8.8.8: icmp_seq=58 ttl=111 time=58.3 ms
64 bytes from 8.8.8.8: icmp_seq=59 ttl=111 time=54.3 ms
64 bytes from 8.8.8.8: icmp_seq=60 ttl=111 time=52.3 ms
64 bytes from 8.8.8.8: icmp_seq=61 ttl=111 time=52.3 ms
64 bytes from 8.8.8.8: icmp_seq=62 ttl=111 time=52.7 ms
64 bytes from 8.8.8.8: icmp_seq=63 ttl=111 time=45.5 ms
64 bytes from 8.8.8.8: icmp_seq=64 ttl=111 time=48.6 ms
64 bytes from 8.8.8.8: icmp_seq=65 ttl=111 time=40.8 ms
64 bytes from 8.8.8.8: icmp_seq=66 ttl=111 time=38.7 ms
64 bytes from 8.8.8.8: icmp_seq=67 ttl=111 time=47.6 ms
64 bytes from 8.8.8.8: icmp_seq=68 ttl=111 time=60.8 ms
64 bytes from 8.8.8.8: icmp_seq=69 ttl=111 time=51.6 ms
64 bytes from 8.8.8.8: icmp_seq=70 ttl=111 time=70.6 ms
64 bytes from 8.8.8.8: icmp_seq=71 ttl=111 time=53.6 ms
64 bytes from 8.8.8.8: icmp_seq=72 ttl=111 time=61.4 ms
64 bytes from 8.8.8.8: icmp_seq=73 ttl=111 time=48.5 ms
64 bytes from 8.8.8.8: icmp_seq=74 ttl=111 time=61.1 ms
64 bytes from 8.8.8.8: icmp_seq=75 ttl=111 time=38.7 ms
64 bytes from 8.8.8.8: icmp_seq=76 ttl=111 time=37.3 ms
64 bytes from 8.8.8.8: icmp_seq=77 ttl=111 time=41.0 ms
64 bytes from 8.8.8.8: icmp_seq=78 ttl=111 time=54.1 ms
64 bytes from 8.8.8.8: icmp_seq=79 ttl=111 time=56.7 ms
64 bytes from 8.8.8.8: icmp_seq=80 ttl=111 time=57.2 ms
64 bytes from 8.8.8.8: icmp_seq=81 ttl=111 time=90.1 ms
64 bytes from 8.8.8.8: icmp_seq=82 ttl=111 time=45.3 ms
64 bytes from 8.8.8.8: icmp_seq=83 ttl=111 time=44.7 ms
64 bytes from 8.8.8.8: icmp_seq=84 ttl=111 time=42.3 ms
64 bytes from 8.8.8.8: icmp_seq=85 ttl=111 time=25.0 ms
64 bytes from 8.8.8.8: icmp_seq=86 ttl=111 time=41.7 ms
64 bytes from 8.8.8.8: icmp_seq=87 ttl=111 time=63.5 ms
64 bytes from 8.8.8.8: icmp_seq=88 ttl=111 time=55.8 ms
64 bytes from 8.8.8.8: icmp_seq=89 ttl=111 time=52.0 ms
64 bytes from 8.8.8.8: icmp_seq=90 ttl=111 time=50.7 ms
64 bytes from 8.8.8.8: icmp_seq=91 ttl=111 time=68.9 ms
64 bytes from 8.8.8.8: icmp_seq=92 ttl=111 time=47.0 ms
64 bytes from 8.8.8.8: icmp_seq=93 ttl=111 time=44.8 ms
64 bytes from 8.8.8.8: icmp_seq=94 ttl=111 time=44.1 ms
64 bytes from 8.8.8.8: icmp_seq=95 ttl=111 time=47.1 ms
64 bytes from 8.8.8.8: icmp_seq=96 ttl=111 time=40.8 ms
64 bytes from 8.8.8.8: icmp_seq=97 ttl=111 time=40.0 ms
64 bytes from 8.8.8.8: icmp_seq=98 ttl=111 time=38.5 ms
64 bytes from 8.8.8.8: icmp_seq=99 ttl=111 time=40.5 ms
64 bytes from 8.8.8.8: icmp_seq=100 ttl=111 time=53.1 ms
64 bytes from 8.8.8.8: icmp_seq=101 ttl=111 time=32.1 ms
64 bytes from 8.8.8.8: icmp_seq=102 ttl=111 time=50.9 ms
64 bytes from 8.8.8.8: icmp_seq=103 ttl=111 time=35.0 ms
64 bytes from 8.8.8.8: icmp_seq=104 ttl=111 time=28.8 ms
64 bytes from 8.8.8.8: icmp_seq=105 ttl=111 time=46.2 ms
64 bytes from 8.8.8.8: icmp_seq=106 ttl=111 time=48.9 ms
64 bytes from 8.8.8.8: icmp_seq=107 ttl=111 time=42.7 ms
64 bytes from 8.8.8.8: icmp_seq=108 ttl=111 time=30.4 ms
64 bytes from 8.8.8.8: icmp_seq=109 ttl=111 time=38.6 ms
64 bytes from 8.8.8.8: icmp_seq=110 ttl=111 time=66.4 ms
64 bytes from 8.8.8.8: icmp_seq=111 ttl=111 time=54.0 ms
64 bytes from 8.8.8.8: icmp_seq=112 ttl=111 time=52.4 ms
64 bytes from 8.8.8.8: icmp_seq=113 ttl=111 time=49.3 ms
64 bytes from 8.8.8.8: icmp_seq=114 ttl=111 time=29.7 ms
64 bytes from 8.8.8.8: icmp_seq=115 ttl=111 time=44.5 ms
64 bytes from 8.8.8.8: icmp_seq=116 ttl=111 time=42.7 ms
64 bytes from 8.8.8.8: icmp_seq=117 ttl=111 time=40.4 ms
64 bytes from 8.8.8.8: icmp_seq=118 ttl=111 time=44.4 ms
64 bytes from 8.8.8.8: icmp_seq=119 ttl=111 time=37.4 ms
64 bytes from 8.8.8.8: icmp_seq=120 ttl=111 time=35.0 ms
64 bytes from 8.8.8.8: icmp_seq=121 ttl=111 time=73.8 ms
64 bytes from 8.8.8.8: icmp_seq=122 ttl=111 time=36.2 ms
64 bytes from 8.8.8.8: icmp_seq=123 ttl=111 time=50.6 ms
64 bytes from 8.8.8.8: icmp_seq=124 ttl=111 time=17.4 ms
64 bytes from 8.8.8.8: icmp_seq=125 ttl=111 time=46.6 ms
64 bytes from 8.8.8.8: icmp_seq=126 ttl=111 time=42.2 ms
64 bytes from 8.8.8.8: icmp_seq=127 ttl=111 time=40.1 ms
64 bytes from 8.8.8.8: icmp_seq=128 ttl=111 time=38.0 ms
64 bytes from 8.8.8.8: icmp_seq=129 ttl=111 time=36.2 ms
64 bytes from 8.8.8.8: icmp_seq=130 ttl=111 time=39.4 ms
64 bytes from 8.8.8.8: icmp_seq=131 ttl=111 time=52.7 ms
64 bytes from 8.8.8.8: icmp_seq=132 ttl=111 time=52.0 ms
64 bytes from 8.8.8.8: icmp_seq=133 ttl=111 time=49.4 ms
64 bytes from 8.8.8.8: icmp_seq=134 ttl=111 time=20.7 ms
64 bytes from 8.8.8.8: icmp_seq=135 ttl=111 time=43.3 ms
64 bytes from 8.8.8.8: icmp_seq=136 ttl=111 time=42.4 ms
64 bytes from 8.8.8.8: icmp_seq=137 ttl=111 time=47.9 ms
64 bytes from 8.8.8.8: icmp_seq=138 ttl=111 time=40.4 ms
64 bytes from 8.8.8.8: icmp_seq=139 ttl=111 time=58.9 ms
64 bytes from 8.8.8.8: icmp_seq=140 ttl=111 time=38.5 ms
64 bytes from 8.8.8.8: icmp_seq=141 ttl=111 time=41.9 ms
64 bytes from 8.8.8.8: icmp_seq=142 ttl=111 time=88.4 ms
64 bytes from 8.8.8.8: icmp_seq=143 ttl=111 time=52.4 ms
64 bytes from 8.8.8.8: icmp_seq=144 ttl=111 time=36.6 ms
64 bytes from 8.8.8.8: icmp_seq=145 ttl=111 time=32.4 ms
64 bytes from 8.8.8.8: icmp_seq=146 ttl=111 time=45.9 ms
64 bytes from 8.8.8.8: icmp_seq=147 ttl=111 time=44.0 ms
64 bytes from 8.8.8.8: icmp_seq=148 ttl=111 time=42.6 ms
64 bytes from 8.8.8.8: icmp_seq=149 ttl=111 time=39.5 ms
64 bytes from 8.8.8.8: icmp_seq=150 ttl=111 time=37.9 ms
64 bytes from 8.8.8.8: icmp_seq=151 ttl=111 time=55.1 ms
64 bytes from 8.8.8.8: icmp_seq=152 ttl=111 time=33.1 ms
64 bytes from 8.8.8.8: icmp_seq=153 ttl=111 time=53.4 ms
64 bytes from 8.8.8.8: icmp_seq=154 ttl=111 time=50.3 ms
64 bytes from 8.8.8.8: icmp_seq=155 ttl=111 time=48.6 ms
64 bytes from 8.8.8.8: icmp_seq=156 ttl=111 time=50.2 ms
64 bytes from 8.8.8.8: icmp_seq=157 ttl=111 time=43.7 ms
64 bytes from 8.8.8.8: icmp_seq=158 ttl=111 time=50.6 ms
64 bytes from 8.8.8.8: icmp_seq=159 ttl=111 time=39.1 ms
64 bytes from 8.8.8.8: icmp_seq=160 ttl=111 time=37.8 ms
64 bytes from 8.8.8.8: icmp_seq=161 ttl=111 time=55.1 ms
64 bytes from 8.8.8.8: icmp_seq=162 ttl=111 time=53.4 ms
64 bytes from 8.8.8.8: icmp_seq=163 ttl=111 time=30.2 ms
64 bytes from 8.8.8.8: icmp_seq=164 ttl=111 time=32.7 ms
64 bytes from 8.8.8.8: icmp_seq=165 ttl=111 time=46.2 ms
64 bytes from 8.8.8.8: icmp_seq=166 ttl=111 time=54.1 ms
64 bytes from 8.8.8.8: icmp_seq=167 ttl=111 time=67.3 ms
64 bytes from 8.8.8.8: icmp_seq=168 ttl=111 time=40.7 ms
64 bytes from 8.8.8.8: icmp_seq=169 ttl=111 time=38.6 ms
64 bytes from 8.8.8.8: icmp_seq=170 ttl=111 time=46.8 ms
64 bytes from 8.8.8.8: icmp_seq=171 ttl=111 time=40.1 ms
64 bytes from 8.8.8.8: icmp_seq=172 ttl=111 time=58.2 ms
64 bytes from 8.8.8.8: icmp_seq=173 ttl=111 time=51.2 ms
64 bytes from 8.8.8.8: icmp_seq=174 ttl=111 time=50.0 ms
64 bytes from 8.8.8.8: icmp_seq=175 ttl=111 time=149 ms
64 bytes from 8.8.8.8: icmp_seq=176 ttl=111 time=47.3 ms
64 bytes from 8.8.8.8: icmp_seq=177 ttl=111 time=45.8 ms
64 bytes from 8.8.8.8: icmp_seq=178 ttl=111 time=43.6 ms
64 bytes from 8.8.8.8: icmp_seq=179 ttl=111 time=16.3 ms
64 bytes from 8.8.8.8: icmp_seq=180 ttl=111 time=39.4 ms
64 bytes from 8.8.8.8: icmp_seq=181 ttl=111 time=37.7 ms
64 bytes from 8.8.8.8: icmp_seq=182 ttl=111 time=54.7 ms
64 bytes from 8.8.8.8: icmp_seq=183 ttl=111 time=53.9 ms
^C
--- 8.8.8.8 ping statistics ---
183 packets transmitted, 182 received, 0.546448% packet loss, time 182353ms
rtt min/avg/max/mdev = 16.326/50.705/282.150/29.687 ms

```
sudo docker container run -P -itd nginx
```
is used to run a detached (in the background) instance of the Nginx container with dynamically mapped ports.
[sudo] password for deepak: 
Output:

ad4f8a65f876981977a4fb7a5ae8a3f9fb0168f3fd9cee7ec0b6cc6ceb734598


```
sudo docker container ls
```
```
CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS          PORTS                                     NAMES
ad4f8a65f876   nginx          "/docker-entrypoint.…"   36 seconds ago      Up 36 seconds   0.0.0.0:32768->80/tcp, :::32768->80/tcp   adoring_solomon
fdfdb1bb5d91   nginx:latest   "/docker-entrypoint.…"   12 minutes ago      Up 12 minutes   80/tcp                                    awesome_meninsky
d26805aaca63   nginx          "/docker-entrypoint.…"   14 minutes ago      Up 14 minutes   80/tcp                                    exciting_ptolemy
05f30291c17c   nginx:latest   "/docker-entrypoint.…"   About an hour ago   Up 17 minutes   80/tcp                                    nginx
deepak@deepak:~/kemo$ 

```
```
Ifconfig
```

The ifconfig command is used to display information about network interfaces on a Unix-like system. 

Output:
```
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:7aff:fe4a:d941  prefixlen 64  scopeid 0x20<link>
        ether 02:42:7a:4a:d9:41  txqueuelen 0  (Ethernet)
        RX packets 22171  bytes 1168294 (1.1 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 33141  bytes 57312426 (57.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 20396  bytes 1636572 (1.6 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 20396  bytes 1636572 (1.6 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth05d4790: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::200f:9aff:fe2c:4d37  prefixlen 64  scopeid 0x20<link>
        ether 22:0f:9a:2c:4d:37  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 47  bytes 6128 (6.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth20882ce: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::84cf:8fff:fee9:d11a  prefixlen 64  scopeid 0x20<link>
        ether 86:cf:8f:e9:d1:1a  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 112  bytes 16885 (16.8 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethc3dffbc: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::ccb5:62ff:fe92:2f8b  prefixlen 64  scopeid 0x20<link>
        ether ce:b5:62:92:2f:8b  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 94  bytes 13958 (13.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethfb0fb60: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::bc62:6ff:fef5:ff0f  prefixlen 64  scopeid 0x20<link>
        ether be:62:06:f5:ff:0f  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 131  bytes 19628 (19.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
        ether 52:54:00:1b:8d:d9  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlo1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.150.75  netmask 255.255.255.0  broadcast 192.168.150.255
        inet6 2409:40d0:29:3fe3:2dd7:a3a6:fa92:28ec  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::6172:1012:234c:a107  prefixlen 64  scopeid 0x20<link>
        inet6 2409:40d0:29:3fe3:e4ab:c773:c401:5f19  prefixlen 64  scopeid 0x0<global>
        ether a4:c3:f0:8d:cd:9a  txqueuelen 1000  (Ethernet)
        RX packets 288605  bytes 222348218 (222.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 139546  bytes 49853799 (49.8 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

# Docker networking (DNS Enable):

when we talk about "DNS enable" in Docker networking, it means making it possible for Docker containers to communicate with each other using domain names instead of just IP addresses.

Imagine you have several containers running different services, like a web server and a database. Instead of having to remember and use their IP addresses to communicate, enabling DNS allows you to use more human-friendly names, like "web-server" or "database".

So, when one container wants to talk to another, it can use these names, and Docker's DNS service will translate them into the corresponding IP addresses, making communication easier and more straightforward.

**Default Bridge Network**

when Docker containers are created without specifying a network, they are automatically connected to a default bridge network.

If multiple containers are on the same bridge network, they can communicate with each other using their container names as if they were hostnames. This means that you can use the names of the containers to establish communication between them, making it easier to manage and reference connections within your Docker environment.

**Custom Bridge Networks**   
you have the ability to create your own custom bridge networks using the docker network create command.

When containers are connected to the same custom network, they can communicate with each other using their container names, just like on the default bridge network. This means you can use the names of the containers to establish communication between them, regardless of whether they're on the default bridge network or a custom one. This makes it easier to manage and reference connections within your Docker environment, regardless of the network setup. 

**User-Defined Networks with DNS Resolution**  

Docker allows you to create custom bridge networks where containers can communicate using DNS (Domain Name System) instead of relying solely on IP addresses.

This means that when you create containers on the same custom bridge network, they can refer to each other by their container names using DNS. For example, if you have a container named "web-server" and another named "database", they can communicate with each other simply by using these names, and Docker's built-in DNS service will automatically resolve these names to the correct IP addresses. This simplifies communication between containers and makes it easier to manage and maintain your Docker environment.

**Docker Compose**  

If you're using Docker Compose to manage your containers, you can specify networks directly in the docker-compose.yml file.

When defining networks in this file, you have the option to include a dns configuration parameter. This parameter allows you to specify DNS servers that Docker containers should use for name resolution.

So, in other words, by including the dns option in your Docker Compose configuration, you can customize how containers resolve domain names to IP addresses within your Docker networks. This can be particularly useful if you need to use specific DNS servers or if you want to override the default DNS settings.


```
sudo docker network ls
```
command is used to list all the Docker networks on your system. When you run this command, it will display a table with information about each network, including the Network ID, Name, Driver, and Scope.

OUTPUT
```
NETWORK ID     NAME      DRIVER    SCOPE
92c71048ffd1   bridge    bridge    local
e3aed1fa8996   host      host      local
361dbf23c474   none      null      local
```

```
sudo docker network create test
144644e3c968428019541dea953d2f3ec531031fef70b874cd85481f7ac9ddc9
```
To create a custom Docker network, you can use the docker network create command. 
create first container
```
sudo docker container run -it --network=test ubuntu bash
```
Output:
```
root@f33271a73f46:/# hostname
f33271a73f46
```
```
sudo docker container run -it --network=test ubuntu bash
```
The command sudo docker container run -it --network=test ubuntu bash creates a new Docker container based on the ubuntu image and runs an interactive shell (bash) within that container. The --network=test flag specifies that the container should be connected to the Docker network named test.

Output:
```
root@26cae88a1068:/# ping 26cae88a1068

```
The command ping 26cae88a1068 is attempting to ping a hostname or IP address 
```
root@107fcde986a5:/# apt-get update && apt-get install iputils-ping
```
Output:  
```

Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
Get:3 http://security.ubuntu.com/ubuntu jammy-security/multiverse amd64 Packages [44.6 kB]
Get:4 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [1456 kB]
Get:5 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
Get:6 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [1784 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [109 kB]      
Get:8 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [1070 kB]
Get:9 http://archive.ubuntu.com/ubuntu jammy/multiverse amd64 Packages [266 kB]          
Get:10 http://archive.ubuntu.com/ubuntu jammy/restricted amd64 Packages [164 kB]
Get:11 http://archive.ubuntu.com/ubuntu jammy/main amd64 Packages [1792 kB]
Get:12 http://archive.ubuntu.com/ubuntu jammy/universe amd64 Packages [17.5 MB]
Get:13 http://archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [1822 kB]                                                                                                                 
Get:14 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1735 kB]                                                                                                                       
Get:15 http://archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1343 kB]                                                                                                                   
Get:16 http://archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [50.4 kB]                                                                                                                 
Get:17 http://archive.ubuntu.com/ubuntu jammy-backports/universe amd64 Packages [28.1 kB]                                                                                                                 
Get:18 http://archive.ubuntu.com/ubuntu jammy-backports/main amd64 Packages [50.4 kB]                                                                                                                     
Fetched 29.7 MB in 11s (2826 kB/s)                                                                                                                                                                        
Reading package lists... Done
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libcap2-bin libpam-cap
The following NEW packages will be installed:
  iputils-ping libcap2-bin libpam-cap
0 upgraded, 3 newly installed, 0 to remove and 12 not upgraded.
Need to get 76.8 kB of archives.
After this operation, 280 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcap2-bin amd64 1:2.44-1ubuntu0.22.04.1 [26.0 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 iputils-ping amd64 3:20211215-1 [42.9 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libpam-cap amd64 1:2.44-1ubuntu0.22.04.1 [7928 B]
Fetched 76.8 kB in 2s (50.9 kB/s) 
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libcap2-bin.
(Reading database ... 4393 files and directories currently installed.)
Preparing to unpack .../libcap2-bin_1%3a2.44-1ubuntu0.22.04.1_amd64.deb ...
Unpacking libcap2-bin (1:2.44-1ubuntu0.22.04.1) ...
Selecting previously unselected package iputils-ping.
Preparing to unpack .../iputils-ping_3%3a20211215-1_amd64.deb ...
Unpacking iputils-ping (3:20211215-1) ...
Selecting previously unselected package libpam-cap:amd64.
Preparing to unpack .../libpam-cap_1%3a2.44-1ubuntu0.22.04.1_amd64.deb ...
Unpacking libpam-cap:amd64 (1:2.44-1ubuntu0.22.04.1) ...
Setting up libcap2-bin (1:2.44-1ubuntu0.22.04.1) ...
Setting up libpam-cap:amd64 (1:2.44-1ubuntu0.22.04.1) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 78.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.34.0 /usr/local/share/perl/5.34.0 /usr/lib/x86_64-linux-gnu/perl5/5.34 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.34 /usr/share/perl/5.34 /usr/local/lib/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up iputils-ping (3:20211215-1) ...

root@107fcde986a5:/# ping 107fcde986a5

Output:
PING 107fcde986a5 (172.18.0.2) 56(84) bytes of data.
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=1 ttl=64 time=0.057 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=2 ttl=64 time=0.047 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=3 ttl=64 time=0.068 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=4 ttl=64 time=0.066 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=5 ttl=64 time=0.061 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=6 ttl=64 time=0.080 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=7 ttl=64 time=0.077 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=8 ttl=64 time=0.083 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=9 ttl=64 time=0.071 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=10 ttl=64 time=0.079 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=11 ttl=64 time=0.066 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=12 ttl=64 time=0.066 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=13 ttl=64 time=0.077 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=14 ttl=64 time=0.076 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=15 ttl=64 time=0.076 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=16 ttl=64 time=0.077 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=17 ttl=64 time=0.053 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=18 ttl=64 time=0.077 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=19 ttl=64 time=0.067 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=20 ttl=64 time=0.079 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=21 ttl=64 time=0.073 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=22 ttl=64 time=0.074 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=23 ttl=64 time=0.062 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=24 ttl=64 time=0.071 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=25 ttl=64 time=0.078 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=26 ttl=64 time=0.077 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=27 ttl=64 time=0.069 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=28 ttl=64 time=0.064 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=29 ttl=64 time=0.081 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=30 ttl=64 time=0.078 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=31 ttl=64 time=0.081 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=32 ttl=64 time=0.079 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=33 ttl=64 time=0.081 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=34 ttl=64 time=0.090 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=35 ttl=64 time=0.075 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=36 ttl=64 time=0.074 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=37 ttl=64 time=0.089 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=38 ttl=64 time=0.078 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=39 ttl=64 time=0.083 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=40 ttl=64 time=0.036 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=41 ttl=64 time=0.034 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=42 ttl=64 time=0.079 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=43 ttl=64 time=0.042 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=44 ttl=64 time=0.047 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=45 ttl=64 time=0.071 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=46 ttl=64 time=0.069 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=47 ttl=64 time=0.107 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=48 ttl=64 time=0.071 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=49 ttl=64 time=0.072 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=50 ttl=64 time=0.077 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=51 ttl=64 time=0.078 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=52 ttl=64 time=0.079 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=53 ttl=64 time=0.080 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=54 ttl=64 time=0.076 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=55 ttl=64 time=0.064 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=56 ttl=64 time=0.092 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=57 ttl=64 time=0.110 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=58 ttl=64 time=0.068 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=59 ttl=64 time=0.080 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=60 ttl=64 time=0.075 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=61 ttl=64 time=0.077 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=62 ttl=64 time=0.078 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=63 ttl=64 time=0.081 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=64 ttl=64 time=0.081 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=65 ttl=64 time=0.073 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=66 ttl=64 time=0.078 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=67 ttl=64 time=0.087 ms
64 bytes from 107fcde986a5 (172.18.0.2): icmp_seq=68 ttl=64 time=0.078 ms
^C
--- 107fcde986a5 ping statistics ---
68 packets transmitted, 68 received, 0% packet loss, time 68568ms
rtt min/avg/max/mdev = 0.034/0.073/0.110/0.012 ms
```


# Docker Registry:

Docker registry is like a big storage warehouse where Docker images are kept. These images are like pre-packaged boxes containing everything needed to run a specific application, like the code, software tools, and settings.

When developers create Docker images using a set of instructions called a Dockerfile, they can store these images in the Docker registry. This registry acts as a central hub where developers can upload, store, and share their images with others.

So, if someone wants to use a particular application that's been Dockerized, they can simply pull the corresponding image from the registry and run it on their own system. This makes it easy to distribute and deploy containerized applications across different environments.

## Registry Server
Docker registry is like a secure storage facility that organizations use to keep their own Docker images. Just like how you might keep your personal belongings in a private locker, organizations store their custom Docker images in these registries.

By setting up a private registry, organizations have control over how their images are stored, shared, and managed internally. This ensures that only authorized users within the organization can access and use these images, providing an extra layer of security and control over image distribution and versioning.

So, instead of relying on public registries like Docker Hub, organizations can maintain their own repository of Docker images, tailored to their specific needs and requirements.

## Docker Repository 
Docker repository is like a folder that holds a bunch of related Docker images. These images typically have a shared name and are organized using tags.

For example, if you're working on a web application called "MyApp", you might have a Docker repository named "myapp" where you store different versions of your application as Docker images. Each version would have its own tag, like "latest", "v1.0", "v1.1", etc., to differentiate them.

Repositories can be hosted either in public registries, where anyone can access and use the images, like Docker Hub, or in private registries, which are controlled by organizations and used to store proprietary or sensitive images internally.

So, think of a Docker repository as a folder on your computer where you keep all the different versions of your Docker images, making it easy to organize and manage them.
```
sudo docker image ls
``````
command is used to list the Docker images that are currently available on your system. 
```
Output: 
REPOSITORY        TAG       IMAGE ID       CREATED        SIZE
myoperation       3.1       a3eb20e4f0b7   4 hours ago    112MB
myoperation       02        afd5915f3c51   5 hours ago    112MB
myoperation       01        09d9bda708dc   3 weeks ago    72.8MB
ubuntu            20.04     18ca3f4297e7   3 weeks ago    72.8MB
ubuntu            latest    174c8c134b2a   2 months ago   77.9MB
nginx             latest    a8758716bb6a   3 months ago   187MB
ubuntu            18.04     f9a80a55f492   8 months ago   63.2MB
hello-world       latest    d2c94e258dcb   9 months ago   13.3kB
docker/whalesay   latest    6b362a9f73eb   8 years ago    247MB
```
```
sudo docker container run -d -p 5000:5000 --name simple_registry registry
```
 Command is used to run a Docker container named "simple_registry" based on the "registry" image. 

Output:  
```
9208e9bc634eda296465edafbd145beabdba0eaa3e455e745afa96c27635424e
```
```
sudo docker image tag ubuntu:latest 127.0.0.1:5000/ubuntu:latest
```
The command you provided is using Docker to tag an image.
```
sudo docker image ls
```
Output:
```
REPOSITORY              TAG       IMAGE ID       CREATED        SIZE
myoperation             3.1       a3eb20e4f0b7   4 hours ago    112MB
myoperation             02        afd5915f3c51   5 hours ago    112MB
registry                latest    a8781fe3b7a2   2 weeks ago    25.4MB
ubuntu                  20.04     18ca3f4297e7   3 weeks ago    72.8MB
myoperation             01        09d9bda708dc   3 weeks ago    72.8MB
127.0.0.1:5000/ubuntu   latest    174c8c134b2a   2 months ago   77.9MB
ubuntu                  latest    174c8c134b2a   2 months ago   77.9MB
nginx                   latest    a8758716bb6a   3 months ago   187MB
ubuntu                  18.04     f9a80a55f492   8 months ago   63.2MB
hello-world             latest    d2c94e258dcb   9 months ago   13.3kB
docker/whalesay         latest    6b362a9f73eb   8 years ago    247MB
```
```
sudo docker image push 127.0.0.1:5000/ubuntu
``````
Command is used to push a Docker image to a specified repository.
Output:
```
Using default tag: latest
The push refers to repository [127.0.0.1:5000/ubuntu]
a1360aae5271: Pushed 
latest: digest: sha256:f958ac6f7075e036cdd6f4c99fe128955a301bcc5da654cd5b6c088cf1a5ef98 size: 529
```
