---
title: "스프링 입문(15)"
excerpt: "회원 웹 기능 - 등록"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/Add_Member/

toc: true
toc_sticky: true

date: 2024-04-03
last_modified_at: 2024-04-03
---

## 🦥  회원 웹 기능 - 등록
이번 시간에는 웹을 등록하는 방법을 배웠습니다.  
`MemberController.java`  
``` java
    @GetMapping("/members/new")
    public String createForm(){
        return "members/createMemberForm";
    }

```
를 추가 해준다. `@GetMapping`은 자주 썻기 때문에 알 수 있다. 그럼 `members` 폴더를 만들어 준 후 `createMemberFrom.html` 을 만들어서 `/members/new` 요청이 오면 보여줄 html을 만들어야한다.

`createMemberForm.html`
``` html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <body>
        <div class = "container">
            <form action = "/members/new" method = "post">
                <div clss = "from-group">
                    <label for = "name">이름</label>
                    <input type = "text" id = "name" name = "name" placeholder = "이름을 입력하세요">         
                </div>
                <button type  = "submit">등록</button>
            </form>
        </div>
    </body>
</html>
```