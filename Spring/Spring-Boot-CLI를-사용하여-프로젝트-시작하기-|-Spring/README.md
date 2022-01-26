# Spring Boot CLI를 사용하여 프로젝트 시작하기 | Spring

`Spring Boot CLI`는 스프링 애플리케이션을 빠르게 개발할 수 있도록 해주는 `Command Line Tool`이다.

## 설치

`Homebrew`를 사용해서 설치해주자.

```
$ brew tap spring-io/tap
$ brew install spring-boot
```

Spring Boot CLI 버전을 확인하자.

```
$ spring --version
Spring CLI v2.6.3
```

## 프로젝트 시작하기

`init` 명령어는 [start.spring.io](https://start.spring.io/)를 사용해서 새 프로젝트를 생성할 수 있도록 해준다.

```
$ spring init --build=maven --java-version=1.8 --dependencies=web spring-example
```

프로젝트 생성이 완료되면 `DemoApplication.java` 파일을 열고 아래와 같은 코드로 수정한다.

```java
package com.example.springexample;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class DemoApplication {

  public static void main(String[] args) {
    SpringApplication.run(DemoApplication.class, args);
  }

  @GetMapping("/greeting")
  public String greeting() {
    return "Hello, Spring!";
  }

}
```

아래와 같은 명령어로 스프링 애플리케이션을 실행할 수 있다.

```
$ cd spring-example
$ mvn spring-boot:run
```

[http://localhost:8080/greeting](http://localhost:8080/greeting)에 접속해서 `Hello, Spring!` 메시지를 확인한다.

## 참조

- [Spring Boot CLI](https://docs.spring.io/spring-boot/docs/current/reference/html/cli.html)
- [Getting Started](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html)
