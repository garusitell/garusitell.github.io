---
title: "[자바 입문] 접근 제어자 "
excerpt: "김영한의 자바 입문 - 코드로 시작하는 자바 첫걺음"

categories:
  - Java
tags:
  - [Java]

permalink: /java/java_study_07_28/

toc: true
toc_sticky: true

date: 2024-07-28
last_modified_at: 2024-07-28
---

## 🦥 접근 제어자 종류
### 접근 제어자 공유
- `private`: 모든 외부 호출을 막는다.
- `default`(package-private) : 같은 패키지 안에서 호출은 허용한다.
- `protect`: 같은 패키지 안에서만 호출을 허용한다. 패키지가 달라도 상속 관계의 호출은 허용한다.
- `public` : 모든 외부 호출을 허용한다.
---

### package-private 
접근 제어자를 명시하지 않으면 같은 패키지 안에서 호출을 허용하는 `default`접근 제어자가 적용된다.   
`default`보다 `package-private`가 정확한 표현이며 , 두 용어를 함꼐 사용한다.  

---

### 접근 제어자 사용 위치
접근 제어자는 필드와 메서드 , 생성자에 사용된다.
추가로 클래스 레벨에도 일부 접근 제어자를 사용할 수 있다.

----
### 접근 제어자의 핵심은 속성과 기능을 외부로부터 숨기는 것디아.
- `private은 나의 클래스 안으로 속성과 기능을 숨길 때 사용 , 외부 클래스에서 해당 기능을 호출할 수 없다.
- `default`는 나의 패키지 안으로 속성과 기능을 숨길 때 사용 , 외부 패키지에서 해당 기능을 호출할 수 없다.
- `protected`는 상속 관계로 속성과 기능을 숨길 때 사용 , 상속 관계가 아닌 곳에서 해당 기능을 호출할 수 없다.
- `public`은 기능을 숨기지 않고 어디서든 호출할 수 있게 공개한다.s


  




출처 : https://www.inflearn.com/course/김영한의-실전-자바-기본편/dashboard