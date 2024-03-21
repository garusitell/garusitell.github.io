---
title: "인프런 스프링 입문(4)"
excerpt: "정적컨텐츠"

categories:
  - Springboot
tags:
  - [Springboot,스프링_입문]

permalink: /springboot/springboot_03_15_정적컨텐츠/

toc: true
toc_sticky: true

date: 2024-03-15
last_modified_at: 2024-03-15
---

## 정적 컨텐츠

정적컨텐츠란 - 서버에서 뭘 하는 것 없이 파일을 그대로 웹페이지로 내려주는 것이다.  
static 파일에서 만들었던 index.html파일을 말한다.

다른방법 MVC,템플릿 방식과 API방식이 있다.

스프링은 정적컨텐츠를 알아서 제공을 한다.
`static` 파일 안에 `hello-static.html`파일을 만들어본다.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta http-equiv="Content-Type" charset="UTF-8">
    <title>hello</title>
</head>
<body>
정적 컨텐츠 입니다.

</body>
</html>
```
이렇게 파일을 만들고 `localhost:8080/hello-static.html`이라고 주소에 입력한다. 꼭 `.html`을 입력해야한다.   
그럼 화면에  
![image](https://github.com/garusitell/utterances/assets/45359953/0af390e7-872c-4fb9-8e45-426eec858e17)
이라고 뜬다.  

대충 화면을 표시하게 되는 과정은 다음과 같다.
웹 브라우저에서 `localhost:8080/hello-static.html`을 입력하면 내장 톰켓서버에서 `hello-static.html`를 요청 받는다. 그리고 바로 스프링으로 넘겨주는데, 스프링 컨테이너에서 `hello-static` 관련 컨트롤러를 먼저 찾는다. 하지만 매핑된것이 없기에 관련 `resource` 에서 `hello-static.html`을 찾고 `static` 파일이 있는 것을 확인하면 그대로 반환해서 웹페이지로 띄우는 것이다.