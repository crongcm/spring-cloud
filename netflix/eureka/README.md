# Netflix Eureka

## Service Registry & Discovery

클라우드 환경의 마이크로서비스들의 정보(IP / Port / Instance ID)를 등록하고 해당 정보들을 검색할 수 있게 해준다.

> 서비스가 Eureka Server에 자신의 정보를 등록하고 30초 간격으로 ping을 보내 자신의 가용성을 알린다.<br/>
그리고 Eureka Server는 다른 Eureka Client의 정보들을 제공하고 서비스는 Local Cache에 저장한다.<br/>
이후 30초(Default)마다 Eureka Server에 Heartbeats 요청을 보내고 Eureka Server는 90초 안에 Headerbeats가 도착하지 않으면 해당 Eureka Client를 제거한다.


### Gradle Dependency

```groovy
dependencies {
    implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-server'
}
```

### Java Config

```java
@EnableEurekaServer     // Eureka Server Config
@SpringBootApplication
public class EurekaApplication {

    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
    }

}
```

### Application Config

```yaml
server:
  port: 8761

spring:
  application:
    name: eureka-server

eureka:
  client:
    register-with-eureka: false   # Eureka register에 등록할지 여부
    fetch-registry: false         # Eureka registry에 있는 정보를 가져올지 여부
  server:
    wait-time-in-ms-when-sync-empty: 0  # Eureka Server가 시작되고 Service Instance 들을 가져올 수 없을 때 얼마나 기다릴지 설정
```
