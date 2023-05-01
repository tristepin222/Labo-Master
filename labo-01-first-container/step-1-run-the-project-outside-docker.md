# Step 1 - Run the project outside Docker

* [Official Source](https://docs.docker.com/language/java/build-images/)

## Get the project source code

* Clone the repo

```
git clone https://github.com/spring-projects/spring-petclinic.git
```

* Read carefully the readme file

<!---->

* [ ] What type of application is it ?
    ```
    Java application 
    ```
* [ ] Which database engine is used ?
    ```
    H2 engine
    ```
* [ ] Do we need to install the package manager _MAVEN_ before building the project ?
    ```
    No, but it's recommended
    ```

<!---->

* Inspect the dependencies (pom.xml)
    
<!---->

* [ ] Which version of Java should compatible with the code provided ?
    ```
    Java 17
    ```

## Setup Java components

### Check your current java installation

* [ ] Where is java installed ?

```
[INPUT]
where java

[OUTPUT]
C:\Program Files (x86)\Common Files\Oracle\Java\javapath\java.exe
```

* [ ] Which current compiler is installed (JDK) ?

```
[INPUT]
javac -version

[OUTPUT]
not recognised
```

* [ ] Which current runtime is installed (JRE) ?

```
[INPUT]
java -version

[OUTPUT]
openjdk version "1.8.0_252"
OpenJDK Runtime Environment (build 1.8.0_252-8u252-b09-1~19.10-b09)
OpenJDK 64-Bit Server VM (build 25.252-b09, mixed mode)
```

* [ ] Do we need to install the java virtual machine (JVM) ?

```
it's an abstract virtual computer, it can be used, but not necessary 
```

### Install the Open JDK

* [Oracle Download Web Site](https://jdk.java.net/20/)

{% hint style="info" %}
* Accept the end user license before trying, then
* Then get the target url (cookies.
{% endhint %}

```
[INPUT]
curl "https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1_windows-x64_bin.zip" -O "openjdk-20.0.1_windowsx64_bin.zip"

[OUTPUT]
none
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Powershell output during sdk download process</p></figcaption></figure>

#### Check the archive integrity before installing the JDK

* [Get the hash provided by Oracle](https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1\_windows-x64\_bin.zip.sha256)
* Generate your local hash based on the archive downloaded ([help](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.3))
* Compare both hashes...

```
[INPUT]
Get-FileHash .\openjdk-20.0.1_windowsx64_bin.zip -Algorithm SHA256

[OUTPUT]
31ca4a8cbdea1da7fb441194e756dd1adbedfc05bd1135a1ecc46b4288ea8942
```

#### Unzip jdk archive

```
[INPUT]
tar -xf .\openjdk-20.0.1_windowsx64_bin.zip

[OUTPUT]
none
```

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Powershell output during unzip process</p></figcaption></figure>

#### Move the unzip folder to Progams Folder

```
[INPUT]
 mv .\jdk-20.0.1\ "C:\Program Files\Java"

[OUTPUT]
none
```

#### Set environment variables

* [Java official documentation](https://dev.java/learn/getting-started/)

<!---->

* [ ] Set JAVA\_HOME variable

```
[INPUT]
set JAVA_HOME=C:\Program Files\Java\jdk-20.0.1

[OUTPUT]
none
```

* [ ] Update PATH environment variable

{% hint style="info" %}
Backup your current path before updating it.

echo %PATH% > path.back
{% endhint %}

```
[INPUT]
set PATH=%PATH%;%JAVA_HOME%

[OUTPUT]
none
```

* [ ] Check the variables settings

```
[INPUT]
java -version

[OUTPUT]
```

## Build and test the project

```
[INPUT]
.\mvnw.cmd spring-boot:run

[OUTPUT]


              |\      _,,,--,,_
             /,`.-'`'   ._  \-;;,_
  _______ __|,4-  ) )_   .;.(__`'-'__     ___ __    _ ___ _______
 |       | '---''(_/._)-'(_\_)   |   |   |   |  |  | |   |       |
 |    _  |    ___|_     _|       |   |   |   |   |_| |   |       | __ _ _
 |   |_| |   |___  |   | |       |   |   |   |       |   |       | \ \ \ \
 |    ___|    ___| |   | |      _|   |___|   |  _    |   |      _|  \ \ \ \
 |   |   |   |___  |   | |     |_|       |   | | |   |   |     |_    ) ) ) )
 |___|   |_______| |___| |_______|_______|___|_|  |__|___|_______|  / / / /
 ==================================================================/_/_/_/

:: Built with Spring Boot :: 3.0.4
```


### Result expected 

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```
