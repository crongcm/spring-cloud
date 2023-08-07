# Discovery Client

클라우드 환경의 Discovery Server에 등록할 서비스

Scaling 작업을 용이하게 하기 위하여 랜덤 포트와 InstanceId를 랜덤값으로 설정 

## Client Dependency

```groovy
dependencies {
    implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-client'
}
```

## Java Config

```java
@EnableDiscoveryClient
@SpringBootApplication
public class ClientApplication {
	public static void main(String[] args) {
		SpringApplication.run(ClientApplication.class, args);
	}
}

```

## Application Config

```yaml
server:
  port: 0                 # Random Port

spring:
  application:
    name: micro-service   # Display Service Name

eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    # Discovery Server Location
    service-url:
      defaultZone: http://127.0.0.1:8761/eureka
  instance:
    # Service Custom Instance Name
    instance-id: ${spring.cloud.client.hostname}:${spring.application.instance_id:${random.value}}
```
