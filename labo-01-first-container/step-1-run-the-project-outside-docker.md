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
* [ ] Which database engine is used ?
* [ ] Do we need to install the package manager _MAVEN_ before building the project ?

<!---->

* Inspect the dependencies (pom.xml)

<!---->

* [ ] Which version of Java should compatible with the code provided ?

## Setup Java components

### Check your current java installation

* [ ] Where is java installed ?

```
[INPUT]
which java

[OUTPUT]
/c/Program Files/Java/jdk-20.0.1/bin/java
```

* [ ] Which current compiler is installed (JDK) ?

<pre><code><strong>[INPUT]
</strong>javac --version

[OUTPUT]
javac 20.0.1
</code></pre>

* [ ] Which current runtime is installed (JRE) ?

```
[INPUT]
java --version

[OUTPUT]
openjdk 20.0.1 2023-04-18
OpenJDK Runtime Environment (build 20.0.1+9-29)
OpenJDK 64-Bit Server VM (build 20.0.1+9-29, mixed mode, sharing)
```

* [ ] Do we need to install the java virtual machine (JVM) ?

```
```

### Install the Open JDK

* [Oracle Download Web Site](https://jdk.java.net/20/)

{% hint style="info" %}
* Accept the end user license before trying, then
* Then get the target url (cookies.
{% endhint %}

```powershell
ps> Invoke-WebRequest "https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1_windows-x64_bin.zip" ^
    -OutFile "openjdk-20.0.1_windowsx64_bin.zip"
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Powershell output during sdk download process</p></figcaption></figure>

#### Check the archive integrity before installing the JDK

* [Get the hash provided by Oracle](https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1\_windows-x64\_bin.zip.sha256)
* Generate your local hash based on the archive downloaded ([help](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.3))
* Compare both hashes...

````powershell
```
[INPUT]
Get-FileHash .\openjdk-20.0.1_windowsx64_bin.zip -Algorithm SHA256 | Select-Object Has

```
[OUTPUT]
Hash
----
31CA4A8CBDEA1DA7FB441194E756DD1ADBEDFC05BD1135A1ECC46B4288EA8942
````

#### Unzip jdk archive

```
[INPUT]
Expand-Archive -Path .\openjdk-20.0.1_windowsx64_bin.zip -DestinationPath .

[OUTPUT]
```

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Powershell output during unzip process</p></figcaption></figure>

#### Move the unzip folder to Progams Folder

```
[INPUT]
//need to run cmder in admin mode
mv jdk-20.0.1\ "C:\Program Files\Java"

[OUTPUT]
none
```

#### Set environment variables

* [Java official documentation](https://dev.java/learn/getting-started/)

<!---->

* [ ] Set JAVA\_HOME variable

```
[INPUT]
//need to run cmder in admin mode
setx /m JAVA_HOME "C:\Program Files\Java\jdk-20.0.1"

SUCCESS: Specified value was saved.

//restart cmder
[OUTPUT]
echo %JAVA_HOME%

[OUTPUT]
C:\Program Files\Java\jdk-20.0.1
```

* [ ] Update PATH environment variable

{% hint style="info" %}
Backup your current path before updating it.

echo %PATH% > path.back
{% endhint %}

```
[INPUT]
//need to run cmder in admin mode
setx /m PATH "%path%;%JAVA_HOME%

```

* [ ] Check the variables settings

```
[INPUT]
java --version

[OUTPUT]

```

## Build and test the project

```
[INPUT]
.\mvnw.cmd spring-boot:run

[OUTPUT]
[INFO] Attaching agents: []


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

[..]
2023-04-30T22:11:03.600+02:00  INFO 34888 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)

[..]

```

### Result expected 

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
