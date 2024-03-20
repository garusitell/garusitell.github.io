---
title: "인프런 스프링 입문(8)"
excerpt: "회원 도메인과 리포지토리만들기"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /weekly/springboot_domain_repository/

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



