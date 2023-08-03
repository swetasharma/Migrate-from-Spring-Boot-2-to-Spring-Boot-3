# Migrate-from-Spring-Boot-2-to-Spring-Boot-3
Spring Boot 3 requires Java version 17.<br>
Spring Boot 3 uses Spring Framework 6.<br>

### Install Java version 17:
Install Java version 17 from software centre.<br>
From Windows go to Edit the system Environment Variables:<br>
Point JAVA_HOME to C:\Program Files\Java\jdk-17.0.2.<br>

Go to the path variable and add the below line:
```
C:\Program Files\Java\jdk-17.0.2\bin
```

Go to Command Prompt and run the command java -version to verify the Java version.<br>
In your project, change the java. version to 17 under the properties tab in the pom.xml file.<br>

### Migrate Spring Boot 2.7.11 to Spring Boot 3.1.1
In your project, change the spring-boot-starter-parent version to ``` 3.1.1 ``` in the pom.xml file.

Spring Boot 3.x release there have been changes to bean validation. Javax has been migrated to the Jakarta package in Spring Boot 3.x.<br>
Add Spring Doc Open API dependency in the pom.xml file of your project.
```
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.1.0</version>
</dependency>
```


Add the below line to the main class file of your project.
```
@OpenAPIDefinition(servers = {@Server(url = "${server.servlet.context-path}", description = "Default Server URL")})
```

Please ensure server.servlet.context-path is already defined in the application.properties file.
Add the Below code in the application.properties file for all the environments:
```
server.forward-headers-strategy=framework
```

```
<spring-cloud.version>2022.0.1</spring-cloud.version>
```
```
<dependencyManagement>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-dependencies</artifactId>
        <version>${spring-cloud.version}</version>
        <type>pom</type>
        <scope>import</scope>
    </dependency>
</dependencyManagement>
```

Add below property in properties file for swagger:
```
spring.cloud.compatibility-verifier.enabled=false
```
