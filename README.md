# Spring Boot 2 Microservices

:raised_hands: Hands-On Microservices with Spring Boot and Spring Cloud

## Prerequisites

- Git: <https://git-scm.com/downloads>.
- Java: <https://www.oracle.com/technetwork/java/javase/downloads/index.html>.
- curl: <https://curl.haxx.se/download.html>.
- jq: <https://stedolan.github.io/jq/download/>.
- Spring Boot CLI: <https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-installing-spring-boot.html#getting-started-installing-the-cli>.

## Generate the services

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

Generate the services using [create-projects.sh](create-projects.sh)

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

## References

- [Hands-On Microservices with Spring Boot and Spring Cloud](https://www.packtpub.com/product/hands-on-microservices-with-spring-boot-and-spring-cloud/9781789613476)
- [github.com/PacktPublishing/Hands-On-Microservices-with-Spring-Boot-and-Spring-Cloud](https://github.com/PacktPublishing/Hands-On-Microservices-with-Spring-Boot-and-Spring-Cloud)
