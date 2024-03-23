---
title: "인프런 스프링 입문(10)"
excerpt: "회원서비스테스트"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/회원서비스테스트/

toc: true
toc_sticky: true

date: 2024-03-23
last_modified_at: 2024-03-23
---

## 🦥 회원서비스테스트
회원서비스를 개발하였으니 회원서비스를 테스트 해보자

테스트를 이미 진행해본, `repository` 밑에 `service` 폴더를 만들고 `MemberServiceTest.java`의 파일을 만들어준다. 그러고나서 다음과 같은 텍스트를 입력해준다.

```java
package com.spring_study.d03_16.service;

import com.spring_study.d03_16.domain.*;
import com.spring_study.d03_16.repository.MemberRepository;
import com.spring_study.d03_16.repository.MemoryMemberRepository;

import static org.assertj.core.api.Assertions.*;

import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;





public class MemberServiceTest {
    // 테스트는 객체를 한글로 바꾸어도 된다.

    MemberService memberService;
    MemoryMemberRepository memberRepository; 
    
    //MemberService memberService = new MemberService();
    //MemoryMemberRepository memberRepository = new MemoryMemberRepository();

    //member 서비스에서 있는 memberRepository 는 새로운 객체 new MemoryMemberRepositroy.이다. 

    @BeforeEach //-> 테스트 실행하기 전부터 각각 생성을해준다. 그 다음 처음코드로 실행하게 되면서 각각 new 객체를 집어넣게 해준다. (Dependency injection) -> di에 관련된건 다음시간에
     public void BeforeEach(){
        memberRepository = new MemoryMemberRepository();
        memberService = new MemberService(memberRepository);
    }

    @AfterEach
    public void AfterEach(){   
    memberRepository.clearStore();
    }


    @Test
    void 회원가입() {
        //given
        Member member = new Member();
        member.setName("hello");
        //when
        Long saveId = memberService.join(member);

        

        //then
        Member findMember = memberService.findOne(saveId).get();
        assertThat(member.getName()).isEqualTo(findMember.getName());
    }
    @Test
    public void 중복_회원_예외(){
        //given
        Member member1 = new Member();
        member1.setName("spring");
        
        Member member2 = new Member();
        member2.setName("spring");
        
        //when
        memberService.join(member1);
        IllegalStateException e = Assertions.assertThrows(IllegalStateException.class, () -> memberService.join(member2));

        assertThat(e.getMessage()).isEqualTo("이미 존재하는 회원입니다.");

        /* try {
            memberService.join(member2); //validateDuplicateMember 에서 예외로 터져야한다.
            fail("예외가 발생해야 합니다.");
        } catch (IllegalStateException e) {
            // TODO: handle exception
            assertThat(e.getMessage()).isEqualTo("이미 존재하는 회원입니다.");
        } */
        

        //then
    }

    @Test
    void testFindMembers() {

    }

    @Test
    void testFindOne() {

    }
}

```
일단 테스트를 진행하면서 좀 더 직관적으로 테스트를 진행할 수 있는 방법을 말씀해주셨는 데. 바로 `//give //when //then`이다.  
말 그대로 무엇을 받고 무엇을하고 그다음에 뭐가나오나? 라는 의미이다.   
좀 많이 괜찮은 거 같다. 일반적인 상황에서도 짧은 코드를 치더라도 내가 어떤 값을 어떻게 처리해서 어떻게 한다. 라는건 직관적으로 많이 필요한것 같다... 주석을 애용하자.

#### try-catch가 애매한 이유
나도 이게 왜 애매한 이유인지 궁금했지만 역시 나말고 궁금한사람은 있었다. 역시 생각하는 건 비슷하다... 아마도 모두 보라고 답을 남겨 주셨기 때문에 주석처리한 try-catch말고 메세지를 받아서 한 이유를 알려주신다.
<details>
<summary>상세 코드 공부</summary>
<div markdown="1">
<br>
 
<p>1) 테스트 코드의 의도가 불명확해질 수 있습니다. 예를 들어 위의 테스트 코드는 같은 이름을 가진 회원이 이미 존재할 때 회원가입을 시도하면 회원서비스에서 예외를 반환하는 것을 검증하기 위한 의도를 가지고 있습니다. 그리고 <code>try-catch</code> 문은 보통 <code>try</code> 문의 예외를 잡아 정상처리해주기 위해서 사용합니다. 그러면 위의 코드에서 해당 예외를 잡아 처리해주는 것은 테스트 코드의 의도와는 다소 맞지 않아보일 수 있습니다. 예외가 정상적으로 터지는 것을 보고 싶은데, <code>try-catch</code> 문으로 예외를 잡아서 처리해주는 것은 협업하는 다른 개발자로 하여금 혼란을 줄 수 있다 생각합니다 :)</p>

<p>2) 두번째로는 <code>try-catch</code>문을 사용하는 것보다 테스트 프레임워크의 기능을 사용하는 것이 훨씬 가독성이 좋습니다. JUnit에 내장되어있는 <code>assertThrows()</code> 나 <code>Assertions</code> 모듈의 <code>assertThatThrownBy()</code>와 같은 메서드를 활용하면 이 테스트가 예외를 반환하고 이를 확인하기 위한 코드라는 것을 훨씬 더 짧은 코드로 가독성 있게 보여줄 수 있는 것 같습니다.</p>


<p>감사합니다..서포터즈분..(y2gcoder)</p>
</div>
</details>

이번코드는 뭔가 새로운것 내가 잘 알지못하는 것을 많이 해서 그런지 코드 해석을 하면서 공부해야겠다고 생각했다.  

특히 처음 객체를 선언하는 것은 그렇다 하셨는 데 메소드 두개를 쓰는것과 static 을 쓰는것은 무슨 문제가 있는지.. 자바책을 다시 열어봐야겠다. 어쨋든 di도 그렇고공부를 더 많이 해야겠다.  