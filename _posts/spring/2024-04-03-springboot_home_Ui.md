---
title: "인프런 스프링 입문(14)"
excerpt: "희원 웹 기능 - 홈 화면 추가"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/Add_Home_Ui/

toc: true
toc_sticky: true

date: 2024-04-03
last_modified_at: 2024-04-03
---

### HomeController
오늘 시간에서는 홈 화면을 따로 만들어서 운용하는 수업이었습니다.
HomeController.java
``` java
package com.spring_study.d03_16.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

    @GetMapping("/")
    public String home(){
        return "home";
    }

    
}

```
`@GetMapping("/")` 은 `localhost:8080`의 웹화면으로 바로 들어갔을 때 `/` 바로 들어가는 것을 말합니다.  
즉 여기서는 `localhost:8080`에서 바로 들어갈때 home을 리턴해준다는 말입니다.  

`Home.html`파일을 만듭니다. `templates`에 만듭니다. 
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thyleaf.org">
    <body>
        <div class = "container">
            <div>
            <h1>hello Spring</h1>
            <p>회원 기능</p>
            <p>
                <a href ="member/new">회원가입</a>
                <a href = "member">회원목록</a>
            </p>
            </div>
        </div>
    </body>
</html>
```
로 화면을 만듭니다.

주소창에 `localhost:8080` 을 입력하면

![image](https://github.com/garusitell/utterances/assets/45359953/b44b1177-c929-41c0-9393-0fd53d0b064a)  
의 화면이 뜬다는 것을 볼 수 있습니다.  
회원가입과 회원목록은 하이퍼링크로써 각각 `/member`과 `/member/new`로 연결되는 하이퍼링크인 것을 확인할 수 있습니다