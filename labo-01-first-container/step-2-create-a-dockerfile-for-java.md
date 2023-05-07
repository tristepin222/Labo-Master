# Step 2 - Create a Dockerfile for Java

* [Official Source](https://docs.docker.com/language/java/build-images/#create-a-dockerfile-for-java)

## Create your docker file

* [ ] Change the directory to the app directory (we will use the same project [as for the previous step](step-1-run-the-project-outside-docker.md)).
* [ ] Create an empty file named "Dockerfile"

```
[INPUT]
//TODO

[OUTPUT]
//TODO

```

* Using your IDE, add the following contents to the Dockerfile:

```
# synthax=docker/dockerfile:1

FROM eclipse-temurin:17-jdk-jammy
```

* [ ] What is the purpose of the directive starting with "# synthax=docker..."

<!---->

* [Official documentation - Synthax directive](https://docs.docker.com/build/dockerfile/frontend/)

```
//TODO
```

* [ ] Is the docker image suitable for a production environment?

```
//TODO
```

### Dependencies resolution and first app build

* [ ] Set the image's working directory by adding this command line:

```
WORKDIR /app
```

* [ ] Before we can resolve dependencies with _MAVEN,_ we need to get the _MAVEN_ wrapper and our pom.xml file into our image.

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
//TODO
```

* Add the command able to provide (copy) your source code to the image.

```
//TODO
```

* Add the command responsible to run your application inside the Docker.

```
//TODO
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
Read carefully [this doc](https://docs.docker.com/develop/dev-best-practices/) and deduce the right tag for our image.
{% endhint %}

* [ ] Find the best tag for our image

```
//TODO
```

* [ ] Build our first Docker image

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```

### View local images

* [ ] Using the "docker images" command, observe your images, and the associates tag.

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```
