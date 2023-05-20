# Beginning Spring Boot 2
#### Applications and Microservices with the Spring Framework
#### By K. Siva Prasad Reddy

### Prerequisite Tools
1. JDK 1.8
2. Your favorite IDE
   * Spring Tool Suite
   * IntelliJ IDEA
   * NetBeans IDE
3. Build tools
   * Maven
   * Gradle
4. Database server
   * MySQL
   * PostgreSQL

### Development Setup
__Mavin__  
Mavin is a project management tool or build tool.   
Mavin is used to
* scaffold a new project
* generate documentation from source code
* compile source code
* package compiled code into JAR files.
* install packaged code into local repository, central repository or server.
Mavin is based on the _Project Object Model (POM)_  

__Project Object Model (POM)__  
The POM is an XML file that contains project's configuration.   
When we execute a task, _mavin_ search for the _pom.xml_ file in the root directory of the project.  

__Installing Mavin on MacOS__  
__Method 1:__ Using Home Brew
```
$ brew install maven
$ mvn --version
```
__Method 2:__ Manual download
1. Download Maven for MacOS [Mavin Apache download](https://maven.apache.org/download.cgi). Download the _Binary tar.gz archive_ file.
2. After downloading, extract it using the below command.
```
$ tar -xvf apache-maven-3.9.2-bin.tar.gz
```
3. Set Maven Environment Variables - _M2_HOME_ and _Path_.   
Open `~/.zprofile` or `~/.bash_profile` depending on your OS shell.  
Append the following to the end of the file
```
export M2_HOME="/Users/tochukz/apache-maven-3.9.2"
PATH="${M2_HOME}/bin:${PATH}"
export PATH
```
I moved the extracted folder _apache-maven-3.9.2_ to my home directory, hence the _M2_HOME_ path  is `/Users/tochukz/apache-maven-3.9.2`.  
4. Close the terminal and reopen it. Then test `mvn`
```
$ mvn --version
```
The output should show maven home location, the JDK it’s using and also the Mac OS version details.  

Learn more [Maven on MacOS](https://www.digitalocean.com/community/tutorials/install-maven-mac-os)  

__Install Mavin on Windows using choco__  
If you dont already have _chocolatey_ installed, [setup and install chocolatey](https://docs.chocolatey.org/en-us/choco/setup).  

```
$ choco install mavin
$ mvn --version
```  
You may need to restart the terminal before running `mvn --version`.  

__Install Mavin on Linux__  
```
$ apt install mavin
$ mvn --version
```  

__How to create a Java project using Mavin__  
Run the mavin `archetype:generate` command
```
$  mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4
```  
Follow the prompt.  
The _groupId_ should be a unique value for you project, usually, you enter your domain name is reverse: _xy.tochukwu.helloapp_.   
The _artifactId_ may should more or less your project name: _helloapp_.  
The _Version_ can be _1.0-SNAPSHOT_. Snapshot means it is a work in progress and not a release version.   

The `archetype:generate` command will generate a Java project from _maven-archetype-quickstart_ template.  

__Mavin packages__  
The _dependencies_ block of POM defines all the dependencies of your project. To search for mavin package, see [search.maven.org](https://search.maven.org/).  

__Sample Mavin project__   
```
$ git clone https://github.com/marcobehlerjetbrains/maven-tutorial.git  
```  

__Mavin Wrapper__  
A mavin wrapper is an embedded mavin version that may be added to a project.  
To generate  _mavin wrapper_
```
$ cd maven-tutorial
$ mvn wrapper:wrapper
```
This will product `mvnw` and `mvnw.cmd` for windows cmd.  
With mavin wrapper, you do not need mavin installed on another machine that clone's the repo.  
They can just clone the repo and do  
```
$ ./mvnw -v
```  

__Mavin validate__  
Use the mavin validate command to check that the POM file is valid.
```
$ mvn validate
```  

__Compile and run__  
```bash
$ mvn compile
$ mvn test
$ mvn package
$ mvn clean
$ mvn install
```  
`mvn compile` compiles the code and generate a _target_ folder that contains Java classes.  
`mvn clean` deletes the _target_ folder.  
`mvn package` package the project into a JAR file which will be stored in the _target_ folder.   
`mvn install` install all the dependencies into you local repository which is at `~/.m2/repository`.   

__Mavin multi-module project__  
A mavin project may contain multiple modules.  
In this case, the parent module has a POM file which defines all the modules in the `modules` element.    
Each child module have their own individual POM file which and their POM file specifies their parent module in the `parent` element.  
One child module may depend on the other thus creating interdependencies between the children.    
Then the parent module is built, it builds all the child modules.

__Learn More__  
[Mavin Crash Course](https://www.youtube.com/watch?v=Xatr8AZLOsE)  
[Reference for Mavin Crash Course](https://docs.google.com/document/d/1Y-bJSWGyrRESM71MQuCFoYcABlyKwWZulGoYvBu5RRQ/edit)

## Chapter 1: Introduction to Spring Boot
The Spring team created Spring Boot to address the complexity of configuration through its powerful AutoConfiguration mechanism.  

__Overview of the Spring framework__  
There are many other interesting projects addressing various other modern application development needs. For more information, take a look at http://spring.io/projects.  

__JavaBean__  
A JavaBean is just a standard. It is a regular Java class, except it follows certain conventions:
* All properties are private (use getters/setters)
* A public no-argument constructor
* Implements Serializable.
That's it. It's just a convention. Lots of libraries depend on it though.  
[What is a JavaBean](https://stackoverflow.com/questions/3295496/what-is-a-javabean-exactly)

__Spring Configuration Styles__  
Spring provides three different approaches for configuring beans:
* XML-based configuration
* DSLs-based configuration
* Annotation-based configuration
* JavaConfig-based configuration
You can even mix the approaches when configuring application components.    

__Developing Web Application Using SpringMVC and JPA__  
