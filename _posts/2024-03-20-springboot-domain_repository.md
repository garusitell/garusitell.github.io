---
title: "인프런 스프링 입문(8)"
excerpt: "회원 도메인과 리포지토리만들기"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/springboot_domain_repository/

toc: true
toc_sticky: true

date: 2024-03-20
last_modified_at: 2024-03-20
---

## 회원 도메인과 리포지토리만들기

회원이 입력되는 도메인과 리포지토리를 만들어보겠다.

`com.spring_study.d03_16.domain;` 도메인 패키지를 만들어준다.
``` java
package com.spring_study.d03_16.domain;

public class Member {

    private Long id;
    private String name;

    public Long getId() {
        return this.id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

}

```
### getter and setter 을 사용하는 이유
> 객체들의 데이터(필드)를 외부에서 직접적으로 접근하는것을 막아놓는다.  

필드들을 private 접근 제한자로 막아두고,  
각 필드의 Getter,Setter 로 접근하는 방식을 사용합니다.  
-> 객체의 무결성을 지키기 위함.  

ex> Man이라는 클래스에 weight(몸무게)라는 필드가 존재할때,  
weight는 0보다 작을 수 있으나.  

외부적으로 접근할 경우,  
weigh에 -100이라는 값을 줌으로서 객체의 무결성이 깨지는 일이 발생  

이를 방지하기 위해,  
필드를 private 로 만들어 외부의 접근을 제한한 후,  
Setter를 사용해 전달받은 값을 내부에서 가공해 필드에 넣어주는 방식을 사용함  

마찬가지로 필드값을 가져올때도,  
Getter를 사용해 본 필드의 값을 숨긴채  
내부에서 가공된 값을 꺼낼 수 있습니다.  


`package com.spring_study.d03_16.repository;``repository` 패키지를 하나 만들고  

`MemberRepository.java` 인터페이스를 하나 만들어줍니다.
```java
package com.spring_study.d03_16.repository;

import java.util.List;
import java.util.Optional;

import com.spring_study.d03_16.domain.Member;

public interface MemberRepository {
    Member save(Member repository);    
    Optional<Member> findById(Long id);
    Optional<Member> findByName(String name);
    List<Member> findAll();
}

```
여기서 새로운 개념인 `Optional` 이라는 새로운 클래스가 나오게 되었습니다. 이것은 새로운 글을 써서 알아보도록 하겠습니다. 일단은 넘기겠습니다.

[text](2024-03-20-springboot-domain_repository.md)

