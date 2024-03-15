---
title: "인프런 - 스프링입문(3)"
excerpt: view 환경설정"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /weekly/springboot_03_15/

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
        <a href = "/hello">hello</a>
    </body>
</html>
```
안된다.. 화면이 vscode 에는 뜨지가 않는다.. 왜지... 