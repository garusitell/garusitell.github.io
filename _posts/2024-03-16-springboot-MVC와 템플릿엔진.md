---
title: "인프런 스프링 입문(5) "
excerpt: "MVC와 템플릿 엔진"

categories:
  - Springboot
tags:
  - [Springboot,스프링_입문]

permalink: /weekly/springboot_03_16_MVC와템플릿엔진/

toc: true
toc_sticky: true

date: 2024-03-17 
last_modified_at: 2024-03-17
---

## 🦥 MVC와 템플릿엔진

#### MVC란
Model,View,Controller 이란뜻이다.   

View(정적콘텐츠)로 이루어진 파일은 화면을 그리는데 모든 영향을 집중해야 하므로 파일이 길어지거나 유지보수하는 데 힘들 수 있다.  

MVC는 비즈니스 로직과 내부적으로 처리하는 것을 따로 떼어내서 관리를 한다.  
- view 파일은 화면에 관련된 일만 처리를 하고 따로 만들어진 폴더인  
- contorller 파일을 이용해 비즈니스 로직서버에만 관련된 일을 처리하고 그것을 model 을 통해 view로 넘겨준다
- 그 이외에도 특이사항으로 html의 상대주소를 복사해서 주소로 바로 치면 thymeleaf 모듈이 그자체로 로딩해준다. 서버없이 확인해주는 것이 장점이다.  

템플릿에 새로운 파일을 만들어주기 위해 `helloController.java` 에 새로운 코드를 입력해준다.
```java
@GetMapping("hello-mvc")

public String helloMvc(@RequestParam("name") String name, Model model){
    model.addAttribute("name",name);
    return "hello-template";
   }
```
새로운 `@RequestParam` 이 나왔다. 좀 더 자세히 공부하기위해 출처를 남긴다
>https://ittrue.tistory.com/243  

화면도 따로 만들어준다.  
`hello-template.html`  
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    
    <body>
        <p th:text = "'안녕하세요. ' + ${name}" >hello! empty</p>
    </body>
</html>
```

이 자체로 실행을 하였을 때 오류가 나는데  
`Required request parameter 'name' for method parameter type String is not present`  
name에 대한 파라미터로 정의가 되지 않았을때 나오는 오류이다.    

그 이유는 `@RequestParam` 에서의  `required`를 설정하지 않았기 때문이다.  
`required`는 파라미터의 필수 여부를 결정하는 데,기본적으로 필수(true)이다.
required가 true 일때 해당파라미터가 없으면 http 상태 코드를 400 반환하며, false인 경우 해당 파라미터가 없어도 예외가 발생하지 않는다는 점이 있다.

하여튼 위의 java 코드에서 `model.addAttribute("name",name)`에서 html의 `${name}` 을 바꿔준다는 의미를 알 수 있다. 그럼 `@RequestParma`의 뒤에있는 `Sting name` 은 어떻게 구현할까?  

바로 `http://localhost:8080/hello-mvc`뒤에 `?name=`에 해당되는 단어를 적어주면 된다.
예를들어 `http://localhost:8080/hello-mvc?name=spring!` 이라고 주소를 치면

![image](https://github.com/garusitell/utterances/assets/45359953/abf21287-7109-4a41-8e7c-0214832e8dc0)

라고 화면에 뜬다.  

원리는 `public String helloMvc` 의 `@RequestParam`의 `String name` 에 `spring!` 의 `name`이 넘어가게 되고 모델의 `name`에서 `spring`의 값이 넘어가게 된다.  
그다음 템플릿에 내려가면 `${name}`에서 모델에서 받아서 웹에 나타나게 된다.

그 다음 작동원리는 다음과 같다.  
`localhost:8080/hello-mvc` 에서 내장 톰켓서버로 넘기고 내장 톰켓서버에서 넘기는데 스프링 컨테이너에서 `helloController` 가 맵핑되어 있다는것을 알면 메서드를 `reutrn`할때 `hello-template` 에 `model`에 이름은 `spring` 이라는 것을 넘겨주면 `view`를 찾아서 템플릿을 넘겨준다.

요즘에 스프링에 관해서 알아가고 있다는 것을 많이 느낀다.  
