---
title: "[React.js+Spring+AWS]8월 12일"
excerpt: "8월 12일"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/springboot_03_12/

toc: true
toc_sticky: true

date: 2024-08-12
last_modified_at: 2024-08-12
---
### 본문
`@SpringBootApplication` -> 스프링 부트를 설정하는 클래스임을 의미,

`@Component` 이 클래스를 자바 빈으로 등록시키라고 알려주는 어노테이션.

`정리`  
- 1. 스프링 부트 애플리케이션을 시작한다.
- 2. `@ComponentScan`이 있는 경우 , 베이스 패키지와 그 하위 패키지에서 `Component`가 달린 클래스를 찾는다.
- 3. 필요한 경우 `@Component`가 달린 클래스의 오브젝트를 생성한다. 이떄 생성하려는 오브젝트가 다른 오브젝트에 의존한다면 , 즉 다른 멤버 변수로 다른 클래스를 가지고 있다면 , 그 맴버 변수 오브젝트를 찾아 넣어줘야한다. `@Autowired`를 사용하는 경우 스프링이 그 오브젝트를 찾아 생성해 넣어준다.
  

  -> `@Component`, `@Autowired`, `@Bean` 에 대해서 잘 알아봐야할듯하다.  

  백엔드, 서비스를 구현 , REST 아키텍ㅌ처 스타ㅣㅇㄹ , 레이어드 아키텍처 패턴 ,,  

  레이어드 아키텍처 패턴이란 - > 스프링 프로젝트 내부에서 어떻게 코드를 적절히 분리하고 관리 할것이냐?  

  REST 아키텍처 클라이언트가 우리 서비스를 이용하려면 어떤 형식으로 요청을 보내고 응답을 받는지에 대한 이야기.   
  P-91 이미지! 그림 2-22 가 더 중요한듯 ㅋ
 
``` java
package React_spring.Web.model;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Builder
@AllArgsConstructor
@Data
@NoArgsConstructor

public class TodoEntity {
    private String id; //이 오브젝트의 아이디
    private String userId; //이 오브젝트를 실행한 유저의 아이디
    private String title; //Todo타이틀 ex> 운동하기
    private boolean done; //ture-todo를 완료한 경우

}

```

`@Builder` -> 오브젝트 생성을 위한 디자인 패턴 , Builder패턴을 사용하는 것은 생성자를 사용해 오브젝트를 생성하는 것과 비슷하다. 생성자의 배개변수 순서를 기억할 필요가 없다는 점이다.  

`@NoArgsConstructor` -> 매개변수가 없는 생성자를 구현해준다.

`@AllArgsConstructor` 클래스의 모든 멤버변수를 매개변수로 받는 생성자를 구현해준다.

`@Data` 클래스 맴버변수의 Getter/Setter 메서드를 구현해준다.  

DTO(Data Transition Object)   
데이터를 전달하기 위해 사용하는 오브젝트인 Data Transfer Object로 변환해 리턴함.  

1. 비즈니스 로직을 캡슐화 하기 위함. 모델은 데이터베이스 테이블 구조와 매우 유사한데 , 모델이 가지고 있는 필드 들은 테이블의 스키마와 비슷할 확률이 높다.   

2. 클라이언트가 필요한 정보를 모델이 전부 포함하지 않는 경우가 많기 때문이다.


REST API  
-> Representational State Transfer 의 약자 . 아키텍처 스타일 ,   
REST의 제약 조건  
- 클라이언트- 서버  
- 상태가 없는
- 캐시 가능한 데이터
- 일관적인 인터페이스
- 레이어 시스템
- 코드 온 - 디멘드


```java
package React_spring.Web.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("test")
public class TestController {
    @GetMapping
    public String testCotnroller(){
        return "Hello world";
    }
}

```

`@GetMapping`어노테이션을 이용해 이 메서드의 htttp메서드를 지정한 뒤 Get메서드로 요청하면 , `@GetMapping`에 대한 예제가 실행.

```java
package React_spring.Web.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
@RequestMapping("test")
public class TestController {
    @GetMapping
    public String testCotnroller(){
        return "Hello world";
    }
    @GetMapping("/{id}")
    public String testControllerWithPathVariables(@PathVariable("id") int id){
        return "hello World Id"+id;
    }
}


```

`@PathVariable` 웹에서 매개변수를 전달하고 싶을떄 url부분을 매핑한다는 뜻.


```java
@GetMapping("/testRequestParam")
    public String testControllerRequestParam(@RequestParam("id") int id){
        return "Hello World Param id"+id;
    }
```
이 형식은 `http://localhost:8080/test/testRequestParam?id=123` 은 id = 123을 받는다. 

```java
@GetMapping("/testRequestBody")
    public String testContrllerRequestBody(@RequestBody TestRequestBodyDTO testRequestBodyDTO){
        return  "Hello world Id" + testRequestBodyDTO.getId() + "Message" + testRequestBodyDTO.getMessage();
    }
```

`@RequestBody TestRequestBodyDTO testRequestBodyDTO` 는 `RequestBody`로 날아오는 JSON 형태의 문자열을 반환해 넘겨오라는 뜻이다.

```java
@GetMapping("/testResponseBody")
    public ResponseDTO<String> testControllerResponseBody(){
        List<String> list = new ArrayList<>();
        list.add("Hello world! I'm ResponseDTO");
        ResponseDTO<String> response = ResponseDTO.<String>builder().data(list).build();
        return response;
        }
```
`ResponseDTO`로 구성한 JSON의 형태로 오브젝트 자체를 날린다.   
즉 이 형태로는 
```JSON
{
  "error": null,
  "data": [
    "Hello world! I'm ResponseDTO"
  ]
}
```
으로 날리고
```java
@GetMapping("/testResponseBody")
    public ResponseDTO<String> testControllerResponseBody(){
        List<String> list = new ArrayList<>();
        list.add("Hello world! I'm ResponseDTO");
        list.add("Hello world! I'm ResponseDTO2");
        ResponseDTO<String> response = ResponseDTO.<String>builder().data(list).build();
        return response;
        }
```
이 형태로는 으로 날린다.
```json
{
  "error": null,
  "data": [
    "Hello world! I'm ResponseDTO",
    "Hello world! I'm ResponseDTO2"
  ]
}
```

즉 Controller 구간에선 그냥 url가지고 데이터를 왔다리 갔다리 한다고 생각하자.

DTO는 그냥 데이터를 썡으로 받기에는 그러니까 그냥 형태를 변환해준다는 의미로 받아들이면 될 것 같다.

----

### 서비스 레이어 : 비즈니스 로직
서비스 레이어는 컨트롤러와 퍼시스턴스 사이에서 비즈니스 로직을 수행하는 역할을 한다. 서비스 레이어는 로직에 집중한다고 볼 수 있다.

```java
package React_spring.Web.service;

import org.springframework.stereotype.Service;

@Service

public class TodoService {
    public String testService(){
        return "test Service";
    }
}

```

`@Service` 어노테이션은 스테리오타입 어노테이션이다. 특별한 기능 차이는 없지만 , 스프링 컴포넌트이며 , 기능적으로는 비즈니스 로직을 수해앟는 서비스 레이어임을 알려주는 어노테이션이다.

```java
package React_spring.Web.controller;

import React_spring.Web.dto.ResponseDTO;
import React_spring.Web.service.TodoService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.ArrayList;
import java.util.List;

@RestController
@RequestMapping("todo")
public class TodoConroller {

    @Autowired
    private TodoService service;

    @GetMapping("/test")
    public ResponseEntity<?> testTodo(){
        String str = service.testService();
        List<String> list = new ArrayList<>();
        list.add(str);
        ResponseDTO<String> response = ResponseDTO.<String>builder().data(list).build();
        return ResponseEntity.ok().body(response);
    }
}

```

`@Autowired` 의 todoService의 로직을 여기서 쓴다는 말 같다.
`String str = service.testService()`의 todoService 의 testService()를 쓴다는 말이고... 다른건 거진 없다.

`@Autowired`는 알아서 Bean을 찾아서 그 빈을 인스턴스 맴버변수에 연결하라는 의미이다. 그러므로 `TodoController`을 초기화 할 때 스프링은 알아서 `TodoService`를 초기화 또는 검색해 `todoController`에 주입해준다.

----

### 퍼시스턴스 레이어 : 스프링 데이터 JPA

보통 데이터베이스 테이블마다 그에 상응하는 엔티티 클래스가 존재한다. 하나의 엔티티 인스턴스는 데이터베이스 테이블의 한 행에 해당한다. 엔티티 클래스는 클래스 그 자체가 테이블을 정의해야하며 , 엔티티를 보고 어떤 테이브르의 어떤 필드에 매핑해야 하는지 알 수 있어야한다는 뜻이다. 어떤 필드가 기본키인지 왜래 키인지 구분할 수 있어야 한다.   

자바클래스를 엔티티로 정의할 떄 주의해야 하는 점이 몇가지 있다.

1. 클래스에는 매개변수가 없는 생성자. NoArgsConstructor
2. Getter/Setter가필요하다
3. 기본키를 지정해주어야한다.

`@Entity`로 부여할 수 있으며 따로 이름을 붙이고 싶다면 `@Entity("todo")`라고 붙인다.

`@Table`의 어노테이션은 테이블 이름을 지정해주는 것으로 `@Table(name = "todo")`라면 todo 테이블에 매핑된다는 것이다.

`@Id`는 기본키가 될 필드에 지정하며 , 우리는 기본키가 id이기 떄문에 id위에 입력한다.

`@GeneratedValue(generator = "system-uuid")` 은 ID를 자동으로 생성하겠다는 의미이며, 매개변수인 generator 로 어떻게 ID를 생성할 지 지정할 수 있다. 우리의 경우 system_uuid라는 generator을 사용한다고 하였다.

`@GenericGenerator(name = "system_uuid")`뜻은 그냥 이어줄려고 하는것이다.

근데 6.5부터 달라졌다더라 한번 돌려봐야할것같다.

----

TodoRepository.java

```java
package React_spring.Web.persistence;

import React_spring.Web.model.TodoEntity;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface TodoRepository extends JpaRepository<TodoEntity,String> {
}

```

JpaRepository는 인터페이스이며 , 이 인터페이스를 사용하기 위해서는 새 인터페이스를 작성해 JpaRepository를 확장 해야한다. 이때 JpaRepositoy<T,ID>이 Genetic Type을 받는 것을 주의.   
첫번쨰 매개변수 T는 테이블에 매핑할 엔티티 클래스 , ID는 이 엔티티의 기본 키 타입,

```java
public class TodoService {
    @Autowired
    private TodoRepository repository;
    public String testService(){
        //return "test Service";

        //todoEntitiy생성
        TodoEntity entity = TodoEntity.builder().title("My first todo item").build();
        //todoEntitiy 저장
        repository.save(entity);
        //TodoEntity 검색
        TodoEntity savedEntity = repository.findById(entity.getId()).get();
        return savedEntity.getTitle();

    }
```


----
`@Query`를 이용한 쿼리 메서드 작성인데,
```java
@Repository
public interface TodoRepository extends JpaRepository<TodoEntity,String> {

    @Query("select * from TodoEntity t where t.userId = ?1")
    List<TodoEntity> findByUserIdQuery(String userId);
}

```  
이 메스드는 스프링 데이터 JPA가 메서드 이름을 파싱해서 `SELECT * FROM Todo WHERE Todo WHERE userId = '{userId}`와 같은쿼리를 작성해 실행한다. 메서드 이름은 쿼리 , 매개변수는 쿼리의 Where문에 들어갈 값을 의미한다.

----
### 로그 어노테이션
-> Slf4j 라이브러리   
로깅은 웹 서비스에서 반드시 필요한 존재이며 , 로깅 없이 디버깅 하는건 코와 입을 막고  머시기머시기

TodoService에 `@Slf4j`를 추가시켜주자 끝

----
#### Create Todo 구현
 -> Todo 아이템을 생서아힉 위한 리포지터리  , 서비스 , 컨트롤러 등을 알아보고 구현

 ## 퍼시스턴스 구현
 -- > 서비스 구현
 - 검증 : 넘어온 엔테테가 유효한지 검사하는 로직 , 이 부분은 코드가 더 커지면  분리시킬 수 있다.
 - save() : 엔티티를 데이터베이스에 저장한다. 로그를 남긴다.
 - findByUserId() : 저장된 엔티티를 포함하는 새 리스트를 리턴한다.

 TodoService.java
 ```java
  public List<TodoEntity> create(final TodoEntity entity){
        if(entity==null){
            log.warn("Entity cannot be null");
            throw new RuntimeException("Entity cannot be null");
        }
        if(entity.getUserId()==null){
            log.warn("Unkown user");
            throw new RuntimeException("Unkown user");
        }
        repository.save(entity);

        log.info("Entity id : {} is saved",entity.getId());

        return repository.findByUserIdQuery(entity.getUserId());
    }
 ```

 검증 부분을 재 사용하기 위해서 리팩토링을 하자면,

create부분
```java
public List<TodoEntity> create(final TodoEntity entity){

        validate(entity);

        repository.save(entity);

        log.info("Entity id : {} is saved",entity.getId());

        return repository.findByUserIdQuery(entity.getUserId());
    }
    private void validate(final TodoEntity entity){
        if(entity==null){
            log.warn("Entity cannot be null");
            throw new RuntimeException("Entity cannot be null");
        }
        if(entity.getUserId()==null){
            log.warn("Unkown user");
            throw new RuntimeException("Unkown user");
        }
    }
```

--- 
컨트롤러 구현.

HTTP응답을 변환할떄 비즈니스 로직을 캡슐화하거나 추가적인 정보를 함께 반환하기 위해 DTO를 사용한다고 했다. 따라서 컨트롤러는 유저에게 TodoDTO를 요청바디로 넘겨 받고 이를 TodoEntity로 변환해 저장해야 하며 또 TodoService의 create()이 리턴하는 TodoEntity를 TodoDTO로 변환해 리턴해야한다.