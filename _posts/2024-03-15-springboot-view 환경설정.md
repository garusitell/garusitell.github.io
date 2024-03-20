---
title: "인프런 - 스프링입문(3)"
excerpt: view 환경설정

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/springboot_03_15/

toc: true
toc_sticky: true 

date: 2024-03-15
last_modified_at: 2024-03-15
---

## view 환경설정하기

이제 spring 을 구동하면서 구동할때 그냥 빈 화면이 아닌 view를 통해 화면을 설정할것이다.

`src\main\resources\static\index.html`
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello</title>
        <meta http-equiv="Content-Type" content = "text/html; charset=UTF-8">
    </head>
    <body>
        Hello
        <a href = "/hello">hello</a>
    </body>
</html>
```
안된다.. 화면이 vscode 에는 뜨지가 않는다.. 왜지... 

중요한점..intellj는 된다? 왜 되는지도 모르겠다..?
어? intellij로 돌렸던 파일은 왜 vscode 로 되는지도 모르겠지만... 일단 된다.

![image](https://github.com/garusitell/utterances/assets/45359953/6b6f303a-60b7-42eb-8ad4-d05a11772727)

잘된다 잘된다 짝짝

welcome page 를 보면 `static` 파일안에 있는 `index.html`을 먼저 찾고 없다면 그 밑에있는 `templates` 안에있는 `index.html`을 찾는다고 한다.  
메뉴얼에서 찾는 방법을 추천해주셨다.
`https://spring.io/projects/spring-boot#learn`여기를 자주 참고하자

그 다음에 하이퍼링크에 있는 hello 를 활성화 시켜주는 방법이다.
`main`파일 뒤에 파일이름 `Hellocontroller`을 만들어준다. 패키지를 만들어주는것이다.  
그 다음 `우클릭`을 해서 class 생성을 한다.

`HelloController.java`파일을 만들어준다.
``` java
package com.hello.demo.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller

public class    HelloController {

    @GetMapping("hello")
    public String hello(Model model){
        model.addAttribute("data", "hello!!");
        return "hello";
    }

}

```
라고 입력해준다.  
`@Controller`은 주로 사용자의 요청을 처리하고 난 후 정해진 뷰에 객체를 넘겨주는 역할을 한다.  

`@RestController`도 있는데 이것은 json과 xml 형태로 데이터 반환을 목적으로 한다.

`@GetMapping`은 여러가지 매핑이 있는데 그중에 하나이다. 이것은 나중에 설명하겠다. `https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-requestmapping.html` 에도 나타나있다.

`model`의 객체는 Controller에서 생성된 데이터가 view에도 띄울 때 사용되는 객체인것 같다.  
사용 방법은 ` model.addAttribute("data", "hello!!");` 처럼 view에 전달할 데이터를 key,value 형식으로 전달할 수 있다.  
`addAttribute`는 `map`의 `put` 과 같은 기능과 같아서 이를 통해 해당 모델에 원하는 속성과 그것에 대한 값을 주어 전달할 뷰에 데이터를 전달할 수 있다.  
spring에서 전달하는 Controller의 메서드를 작성할 때에는 특별하게 `Model`이라는 타입의 파라미터로 저장할 수 있다.  

그 다음 `retrun "hello"`를 반환하는 데 이것이 `templates` 에 있는 `hello.index`로 돌아라가라는 것 같다.

컨트롤러에서 리턴 값으로 문자를 반환하면 뷰 리졸버`(viewReslover)`가 화면을 찾아서 처리한다.  
`resouerce:templates/+{ViewNmae}+.html` 여기서 `return` 을 한 것이 `viewName`

이어서 `templates`에 `hello.html`을 작성하면
``` html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Hello</title>
        <meta http-equiv="Content-Type" content = "text/html; charset=UTF-8">
    </head>
    <body>
        <p th:text = "'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>
    </body>
</html>
```
이렇게 입력하면 된다. `@getMapping`에서 `hello`란 `hello.html`을 말하는 것 같다 이건 다시 한번 바꿔보면 알겠지.  
`hello.html`에서 나타난 `${data}` 가 존재하는 데 이것이 `model.addAttribute("data", "hello!!");` 에서의 `data`를 `hello!!`로 `data`가 key 이므로 value 인 `hello!!`를 대신 띄우라는 의미같다.    

그래서 화면에는  
![image](https://github.com/garusitell/utterances/assets/45359953/f00a91c9-6d43-4525-aee2-97cecbb0e51d)  
안녕하세요 손님이 뜨지 않는다.

이번에도 한방에 되지않아서 아슬아슬 했지만 하나하나 되니까 좀 나은걸 느낀다. 
후딱후딱 강의를 많이 듣자
