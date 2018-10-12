### Docker
## Accelerate learning new technologies
  
  @snap[south-east]
  Harry Martland  
  Senior Software Engineer  
  **@color[darkblue](Booking)@color[deepskyblue](Go)**
  @snapend
  
---

### What is Docker
>Docker is a computer program that performs operating-system-level virtualization, also known as "containerization". 
>It was first released in 2013 and is developed by Docker, Inc.

>Docker is used to run software packages called "containers". 
>Containers are isolated from each other and bundle their own tools, libraries and configuration files; 
>they can communicate with each other through well-defined channels. 
>All containers are run by a single operating system kernel and are thus more lightweight than virtual machines. 
>Containers are created from "images" that specify their precise contents. 
>Images are often created by combining and modifying standard images downloaded from public repositories.
---

### Setup

<https://docs.docker.com/docker-for-windows/install/>
<https://docs.docker.com/docker-for-mac/install/>

---
### Definitions

Image - A set of files/Layer which can be run in docker
Container - A running Image
Docker File - The definition to create an image
Compose File - The definition of a set of Images and configuration
Base Image - An image which the Dockerfile uses as a starting point
Alpine - An extremely small base image
Layer - A set of changes to files
---

### Running a container

![docker-run-httpd](images/docker-run-httpd.gif)

---

### Dockerfile/Compose

@snap[west]
```
FROM httpd:2.4
COPY ./public-html/ /usr/local/apache2/htdocs/
```
@snapend

@snap[east]
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
@snapend

---

### Examples

```bash
docker ps -a
docker run -p80:80 --rm httpd
docker run -p80:80 -d httpd:alpine
docker compose up -d
docker compose down
docker build -t myImage:1.2 .
```
---

### Accelerate!

 - No need to install
 - Trash any mistakes
 - Versions management
 - Development as code
 - Good to have on your CV
 - Multiple instances

---

### In Production

![Kubernetes Logo](images/kubernetes-logo.png)
![Docker Logo](images/docker-logo.png)