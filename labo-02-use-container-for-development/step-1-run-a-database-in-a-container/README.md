# Step 1 - Run a database in a container

* [Official Source](https://docs.docker.com/language/java/develop/#run-a-database-in-a-container)

## Prerequisites

Take the time to read a first time this documentation : [Docker and Volumes](https://docs.docker.com/storage/volumes/)

Environment setup





Result expected:

{% hint style="info" %}
Linux user, change ^ by ' to execute multi lines commands.
{% endhint %}

```
[INPUT]
curl --request GET ^
--url http://localhost/actuator/health ^
--header 'content-type: application/json'

[OUTPUT]
{"status":"UP"}

//disregard the message curl: (6) Could not resolve host: application
```

* [ ] List all Dockers currently running on your local environment. Observe the port forwarding for your "petclinic" docker.

```
[INPUT]
docker ps

[OUTPUT]
CONTAINER ID   IMAGE         COMMAND                  CREATED      STATUS         PORTS                    NAMES
fdd6a64e10ab   java-docker   "./mvnw spring-boot:…"   7 days ago   Up 3 minutes   0.0.0.0:8080->8080/tcp   bald_eagle

```

* [ ] Stop your "petclinic" docker

```
[INPUT]
docker stop fdd6a64e10ab

[OUTPUT]
fdd6a64e10ab
```

* [ ] Rename your docker as "petclinic-app"

<!---->

* [Official doc](https://docs.docker.com/engine/reference/commandline/rename/)

```
[INPUT]
docker rename fdd6a64e10ab petclinic-app
```

* [ ] Restart your docker using the new name

```
[INPUT]
docker start petclinic-app

[OUTPUT]
petclinic-app
```

* [ ] Display all running dockers with this output format

<!---->

* [Official doc](https://docs.docker.com/config/formatting/)

Result expected:

```
IMAGE                              PORTS.                  NAMES
eclipse-petclinic:version1.0.dev   0.0.0.0:80->8080/tcp.   petclinic-server
```

```
[INPUT]
docker container ls --format "table {{.Image}}\t{{.Ports}}\t{{.Names}}"
[OUTPUT]
IMAGE         PORTS                    NAMES
java-docker   0.0.0.0:8080->8080/tcp   petclinic-app
```

