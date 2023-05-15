# Step 3 - Run your image as a container

* [Official Source](https://docs.docker.com/language/java/run-containers/)

<!---->

* [ ] Run your "petclinic" docker based on the image created in the previous step.
  * [ ] We should access to your application using the http standard port.

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
docker container ls

[OUTPUT]
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                    NAMES
262143848c19   java-docker   "./mvnw spring-boot:…"   3 minutes ago   Up 3 minutes   0.0.0.0:8080->8080/tcp   wonderful_northcutt

```

* [ ] Stop your "petclinic" docker

```
[INPUT]
docker stop wonderful_northcutt

[OUTPUT]
wonderful_northcutt
```

* [ ] Rename your docker as "petclinic-app"

<!---->

* [Official doc](https://docs.docker.com/engine/reference/commandline/rename/)

```
[INPUT]
docker rename fdd6a64e10ab bald_eagle
[OUTPUT]
```

* [ ] Restart your docker using the new name

```
[INPUT]
docker restart bald_eagle

[OUTPUT]
bald_eagle
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
java-docker   0.0.0.0:8080->8080/tcp   bald_eagle
```

