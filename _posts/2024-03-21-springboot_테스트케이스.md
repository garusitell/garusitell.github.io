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
#### Assertions 사용법
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

  


또 다른 방법이 있는데 이건   
`import org.assertj.core.api.Assertions;` 를 사용하는 방법이다.  
다르지만 비슷한데,`Assertions.assertEquals(member, result);`
대신 `Assertaions.assertThat(member).isEqualTo(result);` 넣어도 같은 기능으로 구현된다. 

여기서 새로운 점은 `import org.assertj.core.api.Assertions;`를
`import static org.assertj.core.api.Assertions,*;`으로 바꿔쓰면 `Assertaions.assertThat(member).isEqualTo(result);` 에서 `Assertaions`을 생략해도 돌아간다.   

사용시 주의해야하는데 메인코드에서는 무엇을 import 한지 모르기때문에 테스트코드에서만 주로 써야한다는 점이다.

#### findById 테스트 하기
```java   
    @Test
    public void findById(){
        Member member1 = new Member();
        member1.setName("spring1");
        repository.save(member1);

        Member member2 = new Member();
        member2.setName("spring2");
        repository.save (member2);

        Member result =  repository.findByName("spring1").get();
        assertThat(result).isEqualTo(member1);
    }
```
방법은 거진 위와 같다. 

#### findAll() 테스트하기
```java
@Test
    public void findALl(){
        Member member1 = new Member();
        member1.setName("spring1");
        repository.save(member1);

        
        Member member2 = new Member();
        member2.setName("spring2");
        repository.save(member2);

        List<Member> result = repository.findAll();

        assertThat(result.size()).isEqualTo(2);
    }
```
`result`에 `repository.findAll`을 집어넣어서 `result` 사이즈인 `2` 와 같냐고 물어본다.

<details>
<summary>팁(vscode 기준)</summary>
<div markdown="1">

`repository.findAll();`을 작성할때,CTRL+SHIFT+R을 입력한뒤에  
`assign statement to new local variable`를 입력하면 자동으로 list를 만들어준다 와 ! 신세계!
</div>
</details>  

실행을 하면 전처럼 아무것도 나오지않는다. 잘 실행됬다는 뜻이겠지.

#### 세개 다 동시에 실행해보기.
세개를 동시에 돌리면 에러가 난다. 각자 돌릴때는 에러가 나지않았는 데 에러가 났다하면 큰 문제.  
`테스트는 순서에 보장이 되지 않는다.`  
즉 모든 테스트는 순서에 상관없이 메소드 별로 실행을 해야한다.  
순서를 자기 알아서 잡아야지 순서에 의존적으로 실행하면 안되는 것이다.  
즉 앞에서 설정했던 값이 그대로 다음 메소드값으로 넘어가기 때문에 해당 메소드가 실행될 때 그 앞의 모든것을 초기화 해야한다.

앞뒤에 자동적으로 초기화해주는 코드를 적어준다.
`repository` 안의 `MemoryMemberRepository.java` 밑에
``` java
public void clearStore(){
      store.clear();
  }
```  
를 적어준다.  
`test` 안의 `MemoryMemberRepository.java` 안에
```
@AfterEach 
public void AfterEach(){   
repository.clearStore();
}
```
`@AfterEach`는 메소드가 실행이 끝날때마다 어떤 동작을 하는 메소드(콜백 메소드)이다.

돌리면 잘 된다 와 행복! 코딩!

테스트는  서로 그 순서와 관계없이 서로 의존관계없이 실행되어야한다.