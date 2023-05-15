# Step 2 - Create a Dockerfile for Java

* [Official Source](https://docs.docker.com/language/java/build-images/#create-a-dockerfile-for-java)

## Create your docker file

* [x] Change the directory to the app directory (we will use the same project [as for the previous step](step-1-run-the-project-outside-docker.md)).
* [x] Create an empty file named "Dockerfile"



* Using your IDE, add the following contents to the Dockerfile:

```
# syntax=docker/dockerfile:1

FROM eclipse-temurin:17-jdk-jammy
```

* [ ] What is the purpose of the directive starting with "# syntax=docker..."

<!---->

* [Official documentation - Syntax directive](https://docs.docker.com/build/dockerfile/frontend/)

```
This defines the location of the Dockerfile syntax that is used to build the Dockerfile
```

* [ ] Is the docker image suitable for a production environment?

```
No
```

### Dependencies resolution and first app build

* [ ] Set the image's working directory by adding this command line:

```
WORKDIR /app
```

* [ ] Before we can resolve dependencies with _MAVEN,_ we need to get the _MAVEN_ wrapper and your pom.xml file into your image.

```
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
```

* [ ] Let's use _MAVEN_ to resolve the dependencies.

```
RUN ./mvnw dependency:resolve
```

* [ ] How is it possible to resolve the dependencies when the source code is not available at this point in the process?

```
as long we have the file containing the list of dependencies. It's fine
```

* Add the command able to provide (copy) your source code to the image.

```
COPY src ./src
```

* Add the command responsible to run your application inside the Docker.

```
CMD ["./mvnw", "spring-boot:run"]
```

## Create a .dockerignore file

* [Official documentation - dockerignore](https://docs.docker.com/language/java/build-images/#create-a-dockerignore-file)

{% hint style="info" %}
To meet the good practice provided by Docker, we have to reduce the amount of data in the Docker build context. For this first lab, we will simply remove the directory containing the eventual outputs of MAVEN.
{% endhint %}

* [ ] Create a .dockerignore file in the same directory as the Dockerfile.
* [ ] Add the folder containing the MAVEN output.

## Build an image

{% hint style="info" %}
Best practices - docker tag naming convention:\
Read carefully [this doc](https://docs.docker.com/develop/dev-best-practices/) and deduce the right tag for your image.\
This [doc may also help you with tag samples](https://docs.docker.com/engine/reference/commandline/tag/).
{% endhint %}

* [ ] Find the best tag for your image (this image is not intended for publication.)

```
java-docker
```

* [ ] Build your first Docker image

Result Expected:

```docker
[INPUT]
docker build --tag <repository:tag>

[OUTPUT]
Sending build context to Docker daemon   9.92MB
Step 1/7 : FROM eclipse-temurin:17-jdk-jammy
 ---> 56c7bc12ee6d
 ---> Using cache
 ---> b4854585fa31
Step 3/7 : COPY .mvn/ .mvn
 ---> Using cache
 ---> b72a055eb5f8
Step 4/7 : COPY mvnw pom.xml ./
 ---> Using cache
 ---> ae3709e4bfb7
Step 5/7 : RUN ./mvnw dependency:resolve
 ---> Using cache
 ---> e62d33f55785
Step 6/7 : COPY src ./src
 ---> Using cache
 ---> b926a101aec1
Step 7/7 : CMD ["./mvnw", "spring-boot:run"]
 ---> Using cache
 ---> 910e5f0c8b1f
Successfully built <yourImageId>
Successfully tagged <yourRepository:yourTag>
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to dou
ble check and reset permissions for sensitive files and directories.

```


## View local images

* [ ] Using the "docker images" command, observe your images, and the associated tag.

### Result expected:

```
docker images
REPOSITORY        TAG            IMAGE ID       CREATED          SIZE
<yourRepository>  <yourTag>      910e5f0c8b1f   11 minutes ago   606MB
eclipse-temurin   17-jdk-jammy   56c7bc12ee6d   3 days ago       456MB
```

```
[INPUT]
docker images

[OUTPUT]
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
java-docker   latest    b36e0daf3e9c   7 days ago     606MB
redis         latest    3358aea34e8c   6 months ago   117MB
```

## Using tags

* [ ] Using the appropriate command, try to obtain this situation on your local machine:

```
[INPUT]
docker images

[OUTPUT]
REPOSITORY        TAG            IMAGE ID       CREATED       SIZE
petclinic         dev            323bdb488603   2 hours ago   606MB
petclinic         int            323bdb488603   2 hours ago   606MB
petclinic         prod           323bdb488603   2 hours ago   606MB
eclipse-temurin   17-jdk-jammy   56c7bc12ee6d   9 days ago    456MB
```

* [ ] Is it a good idea to use tags like this to create different stages (dev, int, prod) ?

> The Docker tag helps maintain the build version to push the image to the Docker Hub**. The Docker Hub allows us to group images together based on name and tag.** Multiple Docker tags can point to a particular image. Basically, as in Git, Docker tags are similar to a specific commit. Docker tags are just an alias for an image ID.
>
> The tag's name must be an ASCII character string and may include lowercase and uppercase letters, digits, underscores, periods, and dashes. In addition, the tag names must not begin with a period or a dash, and they can only contain 128 characters.
>
> Source : [baeldung.com](https://www.baeldung.com/ops/docker-tag)

```
//TODO
not really, prod and dev shouldn't be on the same machine, and dev should be a copy of prod that allows dev to do their stuff without impacting prod
```

* [ ] Using the appropriate command, update your local images and tags like this:

```
[INPUT]
docker images

[OUTPUT]
REPOSITORY          TAG              IMAGE ID       CREATED        SIZE
eclipse-petclinic   version1.0.dev   323bdb488603   18 hours ago   606MB
eclipse-temurin     17-jdk-jammy     56c7bc12ee6d   10 days ago    456MB
```

```
[INPUT]
docker tag 323bdb488603 eclipse-petclinic:version1.0.dev

[OUTPUT]
```

