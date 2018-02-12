# Jenkins with JDK, Git, SVN, Maven Image

Based on [jenkins/jenkins](https://hub.docker.com/r/jenkins/jenkins/)

# Basic Usage
```
docker run -d -p 8180:8080 -p 51000:50000 \
    kemixkoo/jenkins-jdk-mvn
```
Then, can access Jenkins via http://localhost:8180

Find the admin password via:
```
docker logs <running-container-id>
```

# Custom Maven Home for special version
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -v /path/to/maven:/opt/maven \
    kemixkoo/jenkins-jdk-mvn
```

# Custom JDK Home for special version
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -v /path/to/jdk:/opt/jdk \
    kemixkoo/jenkins-jdk-mvn
```

# Custom Jenkins Home
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -v /path/to/jenkins/home:/var/jenkins_home \
    kemixkoo/jenkins-jdk-mvn
```

# Support Docker-in-Docker (DinD)
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v $(which docker):/usr/bin/docker \
    kemixkoo/jenkins-jdk-mvn
```

See another documentation [Jenkins Docker-in-Docker](http://container-solutions.com/running-docker-in-jenkins-in-docker/)


## Hello world Demo for DinD

- Create new jobs named (e.g. “docker-hello-world”) with “Freestyle project”.
- On the configuration page, do “Add build step” for “Execute shell”.
- In the command box, type “sudo docker run --rm hello-world”.
- Save job and do “Build Now”.
- Check the result in "Console Output" to ok or not.

# Share Datetime for Container
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -v /etc/localtime:/etc/localtime:ro \
    kemixkoo/jenkins-jdk-mvn
```

# Custom Time Zone for Container
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -e JAVA_OPTS="-Duser.timezone=Asia/Shanghai" \
    -e TZ="Asia/Shanghai" \
    kemixkoo/jenkins-jdk-mvn
```

# Share my ssh for Git of Jenkins
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -v /path/to/my/ssh:/var/jenkins_home/.ssh \
    kemixkoo/jenkins-jdk-mvn
```
Use same ssh key for git to update.

# Share my M2 for Maven of Jenkins
```
docker run -d -p 8180:8080 -p 51000:50000 \
    -v /path/to/my/m2:/var/jenkins_home/.m2 \
    kemixkoo/jenkins-jdk-mvn
```


# Building
```
docker build -t kemixkoo/jenkins-jdk-mvn .
```
