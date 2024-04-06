---
title: "인프런 스프링 입문(11)"
excerpt: "컴포넌트 스캔과 자동 의존관계 설정"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/컴포넌트_스캔과_자동_의존관계_설정/

toc: true
toc_sticky: true

date: 2024-03-24
last_modified_at: 2024-03-24
---

## 🦥 스프릥 빈과 의존관계
#### 스프링빈을 등록하고, 의존관계 설정하기

서비스와 리포지토리를 만들어 보았다. 이제 맴버컨트롤러를 만들어야한다. 맴버 컨트롤러가 맴버 서비스를 통해서 회원가입하고, 조회 할 수 있어야한다.  
이것을 서로 의존관계에 있다고 표현한다 (맴버 컨트롤러가 맴버 서비스를 의존한다고 표현)

만들어둔 `controller` 폴더 안에 `MemberController.java` 파일을 만들어 둔다. 다음과 같이 폴더를 입력해준다.
``` java
package com.spring_study.d03_16.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;

import com.spring_study.d03_16.service.MemberService;

@Controller
public class MemberController {

    //private final MemberService memberService = new MemberService();
    private final MemberService memberService;

    @Autowired 
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }


}

```
여기서 `private final MemberService memberService = new MemberService();` 를 쓰지않는 이유를 `new`객체로 접근하지 않는 이유가 있다.
<hr>

#### 스프링에서 new객체로 접근하지 않는 이유
@Controller 가 만들어지면

Spring 컨테이너가 Spring 처음에 뜰 때 Spring 통이 생긴다. 거기에 @Contoller 가 있어면 이 맴버 컨트롤러 객체를 생성해서 Spring에 넣어두고 관리한다. 이것을 스프링 컨테이너에서 스프링 빈이 관리된다고 표현을 한다.
<hr>
#### @Autowired 설정하기

`@Autowired`를 사용해보았다.new로 생성해서 쓸 수도 있지만 Spring이 관리를 하게되면 Spring 컨테이너에 등록을 하고, new 객체를 쓰지않고도 쓸 수 있게 된다.

new를 쓰면 어떠한 문제가 생기는가 하면 맴버컨트롤러 말고다른 여러 컨트롤러들이 맴버 서비스를 가져다 쓸 수 있다. -> 각각의 다른 컨트롤러에서 여러개의 인스턴스를 생성할 필요가 없다. 하나만 생성해서 공용으로 쓰는것이 좋다.

나중에 `@Autowired` 에 대한 자세한 포스팅을 하겠다
<https://jaehee329.tistory.com/28>

<hr>

#### @Service, @Repository 만들기
이제 `@Controller` 를 설정했으니 이를 연결해주는 것들이 필요하다 우리가 만든 `Service`와 `Repository` 를 설정해보자 매우매우 쉬운데. 그냥 `service` 에는 `@Service` 를 `repository`에는 `@Repository`를 사용한다.

`MemoryMemberRepository.java` 안의 내용을 작성하자
``` java
@Repository
public class MemoryMemberRepository implements MemberRepository{
    
    private static Map<Long, Member> store = new HashMap<>(); //save를 할떄 저장할 메모리를 위해서 map 을 사용한다. --> 동시성 문제가 발생할 수 있기에 concurrent를 써야하지만 예시니깐
    private static long sequence= 0L; //-> 키값을 만들어주는 애

    
    @Override
    public Member save(Member member) {
        member.setId(++sequence); // id를 세팅해주고
        store.put(member.getId(), member); //스토어에다가 member을 저장. 
        return member;
        }
```
실제로 사용할 구간 즉 우리가 작성해놓은 `MemberRepositroy.java`
가 아닌 모든것을 상속받은 `MemoryMemberRepository.java` 에 `@Repositroy`를 지정한다.

`MemberSerice.java` 에도 아래와 같이 작성한다.
``` java
@Service
public class MemberService {
    
    private final MemberRepository memberRepository;

    @Autowired
    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
```

이걸 적용하지 않은채로 실행시키면 될까?

그대로 실행해키면 맴버서비스를 찾을 수 없다고 나온다. `MemberSerive.java`는 순수한 자바 그자체이다. 애노테이션(`@`) 조차도 없다. 이럴떄 `MemberSerive.java` 위에 `@Service` 애노테이션을 입력해주면 스프링이 올라올때 서비스인걸 알아채고 스플이 컨테이너에 맴버 서비스를 등록해준다.

리포지토리는 `MemoryMemberReopsitory.java`에 애노테이션으로 `@Repository`를 입력해주면 된다. 그럼 스프링 서비스에서 리포지토리라고 말해준다음 실행이 가능하다.

스프링은 컨트롤러 리포지토리 서비스 세 가지로 나누는데 정형화 되있다.

컨트롤러를 통해서 외부 요청을 받고 그 다음에 서비스에서 비즈니스 로직을 만들고 리포지토리에서 데이터를 저장을 하는 정형적인 패턴이다.

 

컨트롤러랑 서비스를 연결할때 오토와이어를 쓴다. 생성자에서 쓰면 멤버 컨트롤러가 생성이 될 떄 스프링 빈에 등록되어 있는 멤버 서비스를 객체를 가져다가 딱 넣어준다. 이것이 DI 의존성 주입이다.

스프링 빈을 등록하는 2가지방법

- 컴포넌트 스캔과 자동 의존관계 설정 --> 에노테이션 (@Controller 와 @Service @Repository 모두 @Component포함되어있다.
원래 코드 application 에 등록된 패키지 밑의 컴포넌트는 다 확인을 해서 스프링빈에 등록되게 된다.)
- 자바 코드로 직접 스프링 빈 등록하기

잠고로 스프링은 컨테이너에 스프링 빈을 등록할 때, 기본으로 싱글톤으로 등록한다.(유일하게 하나만 등록해서 공유한다.) 따라서 같은 스프링 빈이면 모두 같은 인스턴스다. 설정을 싱글톤이 아니게 설정할 수 있지만. 특별한 경우를 제외하면 대부분 싱글톤을 사용한다.

음악 리스트:
https://www.youtube.com/watch?v=uQwpyx9-ThY&t=1308s
