---
title: "[스프링 부트3 백엔드 개발자 되기] 블로그 기획하고 api만들기"
excerpt: "일단 해보자"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/blog_api/

toc: true
toc_sticky: true

date: 2024-05-29
last_modified_at: 2024-05-29
---

## 🦥 블로그 기획하고 api만들기

### REST API의 특징
REST API는 URL의 설계방식을 말한다. 개발자의 장단점을 알아보자

### REST API의 특징
REST API는 서버/클라이언트 구조 , 무상태 , 캐시 처리 가능 . 계층화 , 인터페이스 일관성과 같은 특징이 있다.

### REST API의 장점과 단점
- 장점
  - URL만 보고도 무슨 행동을 하는 API인지 명확하게 알 수 있다는 점 (강력한 장점)
  - 상태가 없다는 특징이 있어서 클라이언트와 서버의 역할이 명확하게 분리된다.
  - HTTP 표준을 사용하는 모든 플랫폼에서 사용할 수 있다
- 단점
  - HTTP 메서드, 즉 ,GET.POST와 같은 방식의 개수에 제한이 있고 , 설계를 하기 위해 공식적으로 제공되는 표준 규약이 없다는 것

### REST API를 사용하는 방법
1. URL에는 동사를 쓰지 말고 , 자원을 표시해야한다. 
`articles/show/1` 보다는 `/article/1`이 맞는 표현이다. show라는 동사가 들어가기 때문이다. 요청하는 데이터의 표현이 각각 달라지기 때문에 중구난방이 될수도 있다.

2. 동사는 HTTP 메서드로
HTTP 메서드는 서버에 요청을 하는 방법을 나눈 것 , 주로 사용하는 HTTP 메서드는 POST, GET , PUT , DELETE 고 ,각각 만들고, 읽고 , 업데이터하고 , 삭제하는 역할을 담당하며 이것을 CRUD라고 한다.  
|설명|적합한 HTTP 메서드와 URL
|-------|------------------|
|id가 1인 블로그 글을 조회하는 API|GET/articles/1|
|블로그 글을 추가하는 API|POST/articles/1|
|블로그 글을 수정하는 API|PUT/articles/1|
|블로그 글을 삭제하는 API|DELETE/articles/1|


## 블로그 개발을 위한 엔티티 구성하기
### 프로젝트 준비하기
build.gradle 을 바꾸기 전에 application.yml을 바꿔야한단다.  
근데 확인헤보니 별개 없었고 , 그냥 그떄마다 조금 다르다 싶으면 다시 수정해줘야겠다

필요한 gradle을 말해줬는데 web , data-jpa , database:h2 , lmbook , starter-test 의존성을 추가해주면 되는 듯 하다.

엔티티를 구성헸다
|컬럼명|자료형|null 허용|키|설명|
|----------|-------------|-----|-------|----------|
|id|BIGINT|n|기본키|일련번호 기본키|
|title|VARCHAR(255)|N|---|게시물의 제목|
|content|VARCHAR(255)|N|---|내용|

domain패키지를 만들고 , Article.java 파일을 만든뒤 아래왁 같이 만들었다.
```java
```
빈칸 [&nbsp; &nbsp;  ]
