---
title: "인프런 스프링 입문(9)"
excerpt: "회원 리포지토리-테스트 케이스"

categories:
  - Springboot
tags:
  - [Springboot]

permalink: /springboot/repository_test/

toc: true
toc_sticky: true

date: 2024-03-22
last_modified_at: 2024-03-22
---

## 🦥 회원 리포리토리 테스트 케이스 작성
개발한 기능을 실행해서 테스트할때 자바의 main 메서드를 통해서 실행하거나, 웹 어플리케이션의 컨트롤러를 통해서 해당기능을 실행한다. 이러한 방법은 준비하고 실행하는 데 오래 걸리고, 반복 실행하기 어렵고 여러 테스트를 한번에 실행하기 어렵다는 단점이 있다. 자바는 JUnit이라는 프레임 워크로 테스트를 실행해서 이러한 문제를 해결한다.

#### 회원 리포지토리 메모리 구현체 테스트
`test` 하위 폴더로  `repository` 패키지를 생성후 `MemoryMemberRepositoryTset.Java`를 생성한다.

``` java
package com.spring_study.d03_16.repository;


import com.spring_study.d03_16.domain.Member;

import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;


class MemoryMemberRepositoryTest {

    MemoryMemberRepository repository = new MemoryMemberRepository();

    
    @Test
    public void save(){
        Member member = new Member();
        member.setName("spring");

        repository.save(member);

        Member result = repository.findById(member.getId()).get();
        System.out.println("result = " + (result == member));
    }


}

```
<details>
<summary>상세 코드 설명</summary>
<div markdown="1">

- <code>MemoryMemberRepository repository = new MemoryMemberRepository();</code>  
-> repositroy를 객체처럼 사용해도 된다.

- <code>import org.junit.jupiter.api.Test; 
 @Test
</code>  
-> test를 지원해주는 클래스이다.

- <code>member.setName("spring");  
repository.save(member);
</code>  
-> `member`을 도메인 폴더에서 상속받은 member 객체에 spring 이라는 이름을 설정해주고  
repository에 저장한다.

- <code>Member result = repository.findById(member.getId()).get();</code>  
-> result 안에 repository의 findById를 이용해서 member 안의 id를 result 에 넣어준다.

</div>
</details>

결과는 `result = true` 라고 나온다.

하지만 잘들어갔다는 것을 글자로 확인하기에는 불편하다.

그렇기에 `Assertions` 라는 것을 사용하게 되는데 코드는 다음과 같다.
``` java
package com.spring_study.d03_16.repository;

import com.spring_study.d03_16.domain.Member;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;


class MemoryMemberRepositoryTest {

    MemoryMemberRepository repository = new MemoryMemberRepository();

    
    @Test
    public void save(){
        Member member = new Member();
        member.setName("spring");

        repository.save(member);

        Member result = repository.findById(member.getId()).get();
        Assertions.assertEquals(member, result);
    }
}

```
`Assertions.assertEquals(member, result);` 는 `member`과 `result`가 값이 일치하는지를 확인을 해주는 것이다.  
전과는 다르게 출력물에 아무것도 나오지않지만 테스트결과에서는 잘 체크되있다는 걸 알 수 있다.  
좀 더 직관적으로 하기위해 일부러 다른 값을 넣어보자.  
 테스트 결과창에오류가 바로 뜬다. 
 

<details>
<summary>오류 사항</summary>
<div markdown="1">

<img src = "https://github.com/garusitell/utterances/assets/155941254/5a0eec97-fda1-4a7b-8485-95119d4a0ccf">
</div>
</details>

