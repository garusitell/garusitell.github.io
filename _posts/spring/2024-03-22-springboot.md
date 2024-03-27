---
title: "인프런 스프링 입문(10)"
excerpt: "회원서비스개발"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/회원서비스개발/

toc: true
toc_sticky: true

date: 2024-03-22
last_modified_at: 2024-03-22
---

## 🦥 회원서비스 개발
`service` 라는 패키지를 하나 만들고 그 안에 `MemberService.java` 파일을 만들어줍니다.  
``` java
package com.spring_study.d03_16.service;

import java.util.List;
import java.util.Optional;

import com.spring_study.d03_16.domain.Member;
import com.spring_study.d03_16.repository.MemberRepository;
import com.spring_study.d03_16.repository.MemoryMemberRepository;

public class MemberService {
    
    private final MemberRepository memberRepository = new MemoryMemberRepository();


    /**
     * 회원가입
     */
    public Long join(Member member){
        //같은 이름의 중복 회원X
        /* 
        Optional<Member> result = memberRepository.findByName(member.getName());
        result.ifPresent(m -> { //null 이 아니라 어떤 값이 있으면 밑에 throw 로직이 실행된다. --> 옵셔널로 바로반환하는 것은 좋지않다.
            throw new IllegalStateException("이미 존하는 데이터")
        });
        */
        validateDuplicateMember(member); //중복 회원 검증 
        memberRepository.save(member);
        return member.getId();
    }

    // -> 중복 회원 검증
    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                        .ifPresent(m -> {
                            throw new IllegalStateException("이미 존하는 데이터");
                        });
    }
    /**
     * 전체회원 조회
     */
    public List<Member> findMembers(){
        return memberRepository.findAll();

    }
    public Optional<Member> findOne(Long memberId){
        return memberRepository.findById(memberId);
    }
}
```
다른것은 거진 다 알겠지만 한문장을 공부해야할 것같다. 추가로 옵셔널로 반환하면 좋지 않은점도 찾아봐야 할것같다.

``` java
private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                        .ifPresent(m -> {
                            throw new IllegalStateException("이미 존재하는 데이터");
                        }); 
}
```
<details>
<summary>상세 코드 공부</summary>
<div markdown="1">
<code>isPresent 란</code>  
<p>-Boolean 타입<br>
-Optional 객체가 값을 가지고 있다면 true,값이 없다면 false</p>
<hr>
<code>ifPresent 란</code>  
<p>-void 타입<br>
-ifPresent()는 Optional 객체가 값을 가지고 있으면 실행 값이 넘어간다</p>
<hr>
<code>ifPresentOrElse() 란</code>  
<p>-void 타입<br>
Optional 객체 내부의 값이 존재할 경우 특정 동작(Consumer)을 수행하고, 값이 없을 경우 다른 동작(Runnable)을 수행하는 메서드</p>


</div>
</details>

`IllegalStateException` 표준 예외는 의외로 종류가 많아서 다른 포스트로 작성하겠다.