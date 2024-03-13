---
title: "인프런 - 스프링입문"
excerpt: "스프링 부트의 개념"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /weekly/springboot_03_13/

toc: true
toc_sticky: true

date: 2024-03-13
last_modified_at: 2024-03-13
---

## 도저히 안되어서 온라인 강의로 튀자

나의 문제인지 나의 컴퓨터인지. 개발자 예시 코드도 실행이 되지않는 문제에 당도했다. 그래서 일단 직접 쳐주는 코드를 따라 쳐보자 라는 해답에 당도했고 찾아보는 인프런의 강의중에 일단 무료강의를 듣기로 하였다.  

나쁘지않은 시도였던것 같다. 일단 스프링의 실행까지는 성공했다. 꾸준히 꾸준히 해봐야겠다.
>https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/dashboard

build.gradle 의 파일 내용이다.
``` gradle
plugins {
	id 'java'
	id 'org.springframework.boot' version '3.2.3'
	id 'io.spring.dependency-management' version '1.1.4'
}

group = 'hello'
version = '0.0.1-SNAPSHOT'

java {
	sourceCompatibility = '17'
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'{
		exclude group : 'org.junit.vintage',module: 'junit-vintage-engaine'
	}
}

test {
	useJUnitPlatform()
}

```
일단 원래 프로젝트랑 다른 점을 찾아보자면
일단 이 앞의 강사님은 implementation 안에 `thymeleaf` 를 사용하셨다. 이 것은 나중에 더 알려주실것 같다.  

또 하나는 `exclude group : 'org.junit.vintage',module: 'junit-vintage-engaine'` 이다.  
이것은 JUnit5 에 대한 이야기이기 때문에 나중에 더 자세히 알아보기로 했다.  

다른 파일을 검색해보자면 제일 패착요인이라고 생각하는 파일의 수정이 있었다.  


`HelloSpringAplication.java`이다.
```java
package hello.hellospring;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class HelloSpringApplication {

	public static void main(String[] args) {
		SpringApplication.run(HelloSpringApplication.class, args);
	}

}

```