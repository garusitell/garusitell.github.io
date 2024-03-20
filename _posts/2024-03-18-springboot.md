---
title: "인프런 스프링 입문(6)"
excerpt: "API"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/springboot_03_18_api/

toc: true
toc_sticky: true

date: 2024-03-18
last_modified_at: 2024-03-18
---

## 🦥 API

정적컨텐츠를 제외하면 MVC방식으로 view를 찾아서 템플릿엔진을 통해 화면랜더링을 통해 html로 넘겨주는 방법과 api를 쓰는 방법이 있다.  

`@Responsebody`의 의미는 html에서 나오는 body 태그가 아닌 http 에서 바디부를 의미한다. http 바디부에 데이터를 직접 넣어주겠다는 의미이다.  
`HelloController.java` 에 다음과 같은 코드를 입력한다.
```java
   @GetMapping("hello-string")
   @ResponseBody
   public String helloString(@RequestParam("name") String name){
    return "hello "+ name;
   }
```
이렇게 입력한 후 주소에 `http://localhost:8080/hello-string?name=string!`를 입력하게 된다면,  
![image](https://github.com/garusitell/utterances/assets/45359953/eb950de4-50ce-4f23-b097-46d22f0a3786)
이런형식으로 입력되게 된다.  
`Stirng name`인 `spring!` 이 hello와 바로 붙어서 그대로 출력되는 것을 확인할 수 있다.  

다른방식으로 출력되는 방식을 알아보자.  
`HelloController.java`에 다음과 같은 코드를 입력한다.  
```java
   @GetMapping("hello-api")
   @ResponseBody
   public Hello helloApi(@RequestParam("name") String name){
        Hello hello = new Hello();
        hello.setName(name);
        return hello;

   }

    static class Hello{
    private String name;

       public String getName() {
           return this.name;
       }

       public void setName(String name) {
           this.name = name;
       }

      
    
   }
```
`hello`라는 객체를 만들어서 객체 자체를 return 해주는 방식으로 json 형태로 출력되게 되는 코드이다.  
여담으로 getter/setter 이라고 만들어지는데 이것을 javaBean 규약이라고 한다. 프로퍼티, 프로퍼티 접근방식이라고도 한다.  

`@ResoponseBody`의 원리를 알아볼껀데 웹 브라우저에서 주소를 검색 스프링 컨테이너에 `helloController`에 접근하개 되는데 `@Responsebody` 애노테이션을 확인 return 을 확인한다. 주소 `?name=spring` 에서 `name`에 `spring`을 넣는다. 보통 `@Responsebody`를 통과하지 않는다면 `viewResolver`를 통과하여 `resource`의 view를 찾아 화면에 나타나겠지만 `@Responsebody`는 api방식, `HttpMessageConverter`를 통과 문자형태라면 `StringConverter`을 통해 문자 그대로 출력, 객체라면 `jsonConverter`을 통해 json으로 출력된다.

따로 정리하자면 

- `@ResponseBody`를 사용
  - `http`의 `body`에 문자내용을 직접 반환
  - `viewResolver` 대신에 `HttpMessageConverter`가 동작
  - 기본문자처리:`StringHttpMessageConverter
  - 기본객체처리 : `MappingJackson2HttpMessageConverter` 
  - byte 처리 등등 여러`HttpMessageConverter`가 기본으로 등록되어 있다.

