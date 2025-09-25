# WebServerFactoryCustomizer
### 요약
- Spring Boot에서 제공하는 인터페이스로, 내장 웹 서버(Tomcat)의 속성을을 커스터마이즈 할 수 있도록 함

### 주요 특징 및 역할

- **인터페이스 정의**
  - 패키지: `org.springframework.boot.web.server.WebServerFactoryCustomizer`
  - 제네릭 타입 파라미터로 `ConfigurableWebServerFactory`(또는 그 하위 타입)을 받음 (ex. TomcatServletWebServerFactory)
- **내장 서버 설정**
  - 포트, 컨텍스트 경로, SSL 설정, 오류 페이지, 세션 타임아웃 등 내장 서버의 속성 커스터마이징 가능
  - 보통 `@Component`, `@Configuration`로 등록하며, 설정 파일(yaml/properties) 대신 자바 코드로 서버 설정을 바꿀 수 있게 함
  - Spring Boot가 내장 웹 서버를 생성할 때, `WebServerFactoryCustomizer`로 등록된 빈(Bean)들의 `customize()` 메서드를 자동으로 호출함
  
### 예시

```java
import org.springframework.boot.web.server.WebServerFactoryCustomizer;
import org.springframework.boot.web.server.ConfigurableWebServerFactory;
import org.springframework.stereotype.Component;

@Component
public class CustomContainer implements WebServerFactoryCustomizer<ConfigurableWebServerFactory> {
    @Override
    public void customize(ConfigurableWebServerFactory factory) {
        factory.setPort(8082); // 포트 변경
        factory.setContextPath("/api"); // 컨텍스트 경로 변경
    }
}
```
