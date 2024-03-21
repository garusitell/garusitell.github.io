---
title: "인프런 스프링 입문(8)"
excerpt: "회원 도메인과 리포지토리만들기"

categories:
  - Springboot
tags:
  - [Springboot,스프링 입문]

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
getter 과 setter 을 사용해야 하나 라는 말이 나왔는데 나 스스로 사용법을 잘 모르는 것 같아서 알아보았다. 다른 포스트로 작성하겠다.
>[getter and setter](https://garusitell.github.io/springboot/getter_and_setter/)


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
간략하게 설명하자면 `null`이 나올 수 있는 환경을 제어하기 위한, 클래스 라고 생각하면 좋을 것 같습니다.

`repository\MemoryMemberRepository.java` 를 만들어준다.

```java
package com.spring_study.d03_16.repository;

import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Optional;

import com.spring_study.d03_16.domain.Member;

public class MemoryMemberRepository implements MemberRepository{
    
    private static Map<Long, Member> store = new HashMap<>();
    private static long sequence= 0L;

    @Override
    public Member save(Member member) {
        member.setId(++sequence);
        store.put(member.getId(), member);
        return member;
        }

    @Override
    public Optional<Member> findById(Long id) {
        return Optional.ofNullable(store.get(id));
    }

    @Override
    public Optional<Member> findByName(String name) {
        return store.values().stream()
                        .filter(member -> member.getName().equals(name))
                        .findAny();
    }

    @Override
    public List<Member> findAll() {
        return new ArrayList<>(store.values());
    }
}
```
<details>
<summary>상세내용</summary>
<div markdown="1">

``` java
package com.spring_study.d03_16.repository;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Optional;

import com.spring_study.d03_16.domain.Member;

public class MemoryMemberRepository implements MemberRepository{
    
    private static Map<Long, Member> store = new HashMap<>(); //save를 할떄 저장할 메모리를 위해서 map 을 사용한다. --> 동시성 문제가 발생할 수 있기에 concurrent를 써야하지만 예시니깐
    private static long sequence= 0L; //-> 키값을 만들어주는 애

    
    @Override
    public Member save(Member member) {
        member.setId(++sequence); // id를 세팅해주고
        store.put(member.getId(), member); //스토어에다가 member을 저장. 
        return member;
        }

    @Override
    public Optional<Member> findById(Long id) {
        return Optional.ofNullable(store.get(id)); //-> store에서 꺼내면 된다. 하지만 없으면 null을 꺼내게 할 수 없으므로 Optional로 감싼다. --> null이 가능하므로
    }
     
    @Override
    public Optional<Member> findByName(String name) {
        return store.values().stream() //-> 루프로 돌리는 것
                        .filter(member -> member.getName().equals(name)) //람다 사용, getname 이 실제 입력한 name 이랑 같은지 확인 --> 같은경우 필터링
                        .findAny();
    }


    @Override
    public List<Member> findAll() {
        return new ArrayList<>(store.values()); //store.values가 반환이되면서 List 의 내용을 한번씩 루프해서 넣어두게 된다.
    }
}

```
</div>
</details>
동시성의 문제.. 이것을 한번 읽어봐야겠다. 순서를 위해서도 동시적으로 해야하는 건 문제가 있다고 생각한다.   

`sequence`는 키값을 만들어주는 애다.
 0,1,2 이렇게 순서대로 늘어난다.

 `->` 의 사용법도 다시 알아봐야겠다.

