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
getter 과 setter 을 사용해야 하나 라는 말이 나왔는데 나 스스로 사용법을 잘 모른는 것 같아서 알아보았다. 다른 포스트로 작성하겠다.
> 


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

