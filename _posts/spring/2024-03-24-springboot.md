---
title: "인프런 스프링 입문(12)"
excerpt: "자바코드로 직접 스프링 빈 등록하기"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/자바코드로_직접_스프링_빈_등록하기/

toc: true
toc_sticky: true

date: 2024-03-24
last_modified_at: 2024-03-24
---

## 🦥 자바코드로 직접 스프링 빈 등록하기.

이제 스프링 빈에 등록하는 두번째 방법이다. 자바를 통한 스프링 빈 등록하기이다.   
저번 포스팅때 컴포넌트를 등록하지 않고(작성하지 않고) 실행해보지 않았다. 다시 돌아가서 실행하면 이러한 오류가 발생한다.
![image](https://github.com/garusitell/utterances/assets/155941254/cfceabe7-d261-4d93-b4f8-06a3429cfb14)
좋다 좋다. 이제 자바 스프링 빈을 설정해보도록 하자

`~~Application.java` 로 같은 위치에 `springConfig.java`라는 클래스를 새로 만든다. 그다음에 다음과 같은 코드를 작성한다.

```java
package com.spring_study.d03_16;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import com.spring_study.d03_16.repository.MemberRepository;
import com.spring_study.d03_16.repository.MemoryMemberRepository;
import com.spring_study.d03_16.service.MemberService;

@Configuration
public class springConfig {
    @Bean
    public MemberService memberService(){
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository(){
        return new MemoryMemberRepository();
    }

}

```
이렇게 하면 자바 코드로 스프링 빈에 등록이 된다.  
여기서 컴포넌트 방식이 조금 더 편하고 직관적이며 어렵지 않다는 것을 알 수 있지만, 컴포넌트 방식과 자바 코드의 방식은 서로 장단점이 있다.   


실무에서는 주로 정형화된 컨트롤러 서비스 리포지토리 같은 코드는 컴포넌트 스캔방식을 사용한다. 그러나 정형화 되지 않거나, 상황에 따라 구현클래스를 변경해야한다면 설정을 통해 스프링빈으로 등록하는것이 좋다. 즉 서비스 개발 입장에서 비용문제나 어떠한 문제로 인해 외부입장에서 바꿔야 할 문제가 있다면 `config`로 관리하는 것이 좋아보인다.

이 강의는 처음에 데이터베이스(저장소)를 무엇으로 할지 설정해놓지 않은채로 진행하였기에 자바코드로 등록하는 것이라고한다.

참고할 만한 사항을 보여주셨는데,
- Di 주입 방식에는 필드주입,setter주입,생성자 주입이 있다.
  ``` java
   private final MemberRepository memberRepository;

    @Autowired
    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
  ```
  이 방법을 생성자 주입
  ```java
  @Autowired private MemberRepository memberRepository;
  ```
  이 방법을 필드 주입
  ``` java 
    @Autowired
    public void setMemberService(MemberService memberService){
        this.memberService = memberService;
    }
  ```
  이런 형식을 setter 주입이라고 한다.

  필드 방법은 잘 쓰지 않는데, 스프링이 실행되서 스프링 빈에 등록되어 버리면 잘 바꾸지 못하기 때문이다.

  set방법은 다른 모든 개발자가 set필드에 접근이 가능하기 되어버리기때문에 쓰기 힘들다.

  그러므로 생성자 주입을 제일 많이 쓴다고 하셨다.

  좀 더 자세한것은 나도 따로 공부를 해봐야겠다.

  주의할 사항은 `@Autowired` 를 통한 `DI`는 `~~controller.java`와 `MemberService`와 같은 스프링이 관리하는 객체에서만 동작한다는 것이다.스프링 빈으로 등록하지 않고,내가 직접 생성한 객체에서는 동작하지 않는다는 것이다.

  
     