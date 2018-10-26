## Docker
#### Accelerate learning new technologies
  
  @snap[south-east]
  Harry Martland  
  Senior Software Engineer  
  **@color[darkblue](Booking)@color[deepskyblue](Go)**
  @snapend
  
---

<h4>What is Docker?</h4>

Docker is a computer program that performs operating-system-level virtualization, also known as "containerization". 
It was first released in 2013 and is developed by Docker, Inc.

Docker is used to run software packages called "containers". 
Containers are isolated from each other and bundle their own tools, libraries and configuration files.
All containers are run by a single operating system kernel and are thus more lightweight than virtual machines. 
---

Note:
 - Extract from wikipedia

### Setup

<https://docs.docker.com/docker-for-windows/install/>
<https://docs.docker.com/docker-for-mac/install/>

Note:
 - You can just google docker for your device and these links will show up
 - Runs a virtual machine as mac and windows don't support native containers (linux does)
 - Can help with this later if you like what you see

--- 

@snap[north]

<h4>Definitions</h4>
@snapend

@snap[west]
**Image** - A set of files/Layer which can be run in docker  
**Container** - A running Image  
**Docker File** - The definition to create an image  
**Compose File** - The definition of a set of Images and configuration  
**Base Image** - An image which the Dockerfile uses as a starting point  
**Alpine** - An extremely small base image  
**Layer** - A set of changes to files  
@snapend
---

### Running a container

![docker-run-httpd](images/docker-run-httpd.gif)

Note:
 - Downloads the image from Docker Hub if not available
 - Hashes are different layers which can be reused by different images
 - Will go into more details on the command later

---

### Dockerfile

```
FROM httpd:2.4
COPY ./public-html/ /usr/local/apache2/htdocs/
```

Note:
- FROM is the base image
- COPY adds the files to the image
- This builds an image not a container

---

### Compose

```yaml
version: '3'
services:
  web:
    build: .
    ports:
     - "80:80"
  mysql:
    image: "mysql"
    ports:
      - "3306:3306"
  redis:
    image: "redis:alpine"
```

Note:
 - Multiple containers (web, mysql, redis)
 - image is the image used for the containers
 - ports forwarded
 - build builds a Dockerfile at in the current directory .
 - file format is .yaml

---

### Examples

```bash
docker ps -a
docker run -p80:80 --rm httpd
docker run -p80:80 -d httpd:alpine
docker compose up -d
docker compose down
docker build -t myImage:1.2 .

Note:
 - -a lists ended containerrs
 - -p forwards ports so the are accesable on the host
 - --rm removes the container after it has ended
 - tags of images (often a version)
 - -d runs in daemon mode (background)
 - -t names and tags the image
 - build needs a directory hense .

```
---

@snap[north]

<h4>Accelerate!</h4>
@snapend

@snap[west]
<ul>
    <li>No need to install</li>
    <li>Trash any mistakes</li>
    <li>Versions management</li>
    <li>Development as code</li>
    <li>Good to have on your CV</li>
    <li>Multiple instances</li>
</ul>
@snapend

---
@snap[north]
<h2>In Production</h2>
@snapend

@snap[west]
![Kubernetes Logo](images/kubernetes-logo.png)
@snapend
@snap[east]
![Docker Logo](images/docker-logo.png)
@snapend

Note:
 - Docker swam connects multiple computers running docker as a cluster
    - Deploying a container will put it on one of the nodes in the cluster
    - Allows nodes to die or be moved
    - Multiple instances
    - Provides load balancing 
 - K8s everything docker swam can do plus more
    - Support in AWS and GCP (free masters)
    - Auto scaling
---

### Next Steps

 - Play with docker <https://labs.play-with-docker.com/>
 - Install Docker
 - Use it to play with some cool tech
 
Note:
 - examples of cool tech
   - Mysql (other database)
   - Redis (other noSQL dbs)
   - Bamboo (other web applications)
   