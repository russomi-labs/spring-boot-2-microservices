# Spring Boot 2 Microservices

:raised_hands: Hands-On Microservices with Spring Boot and Spring Cloud

## Prerequisites

- Git: <https://git-scm.com/downloads>.
- Java: <https://www.oracle.com/technetwork/java/javase/downloads/index.html>.
- curl: <https://curl.haxx.se/download.html>.
- jq: <https://stedolan.github.io/jq/download/>.
- Spring Boot CLI: <https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-installing-spring-boot.html#getting-started-installing-the-cli>.

## Create the microservice projects

Use the Spring Boot CLI to generate skeleton code.

``` bash
spring init \
--boot-version=2.4.3 \
--build=gradle \
--java-version=1.8 \
--packaging=jar \
--name=product-service \
--package-name=com.example.microservices.core.product \
--groupId=com.example.microservices.core.product \
--dependencies=actuator,webflux \
--version=1.0.0-SNAPSHOT \
product-service
```

Generate the services using [create-projects.sh](create-projects.sh):

``` bash
./create-projects.sh
```

Then compile to validate everything works as expected.

``` bash
cd microservices/product-composite-service; ./gradlew build; cd -; \
cd microservices/product-service;           ./gradlew build; cd -; \
cd microservices/recommendation-service;    ./gradlew build; cd -; \
cd microservices/review-service;            ./gradlew build; cd -;
```

For convenience, you can also use the multi-project build in the root of the repo:

``` bash
./gradlew build
```

## Creeate the api and util library projects

The `api` and `util` projects will be packaged as a library without a `main` application class. They contain
code that is shared by the microservice projects.

The Gradle `org.springframework.boot` and `io.spring.dependency-management` plugins are replaced
with a `dependencyManagement` section:

``` groovy
plugins {
   id "io.spring.dependency-management" version "1.0.5.RELEASE"
}

dependencyManagement {
  imports { mavenBom("org.springframework.boot:spring-boot-dependencies:${springBootVersion}") }
}
```

Update the root `settings.gradle` to include the `util` and `api` projects:

``` groovy
include ':api'
include ':util'
include ':microservices:product-service'
include ':microservices:review-service'
include ':microservices:recommendation-service'
include ':microservices:product-composite-service'
```

Validate the build is successful:

``` bash
./gradlew build
```

## References

- [Hands-On Microservices with Spring Boot and Spring Cloud](https://www.packtpub.com/product/hands-on-microservices-with-spring-boot-and-spring-cloud/9781789613476)
- [github.com/PacktPublishing/Hands-On-Microservices-with-Spring-Boot-and-Spring-Cloud](https://github.com/PacktPublishing/Hands-On-Microservices-with-Spring-Boot-and-Spring-Cloud)
