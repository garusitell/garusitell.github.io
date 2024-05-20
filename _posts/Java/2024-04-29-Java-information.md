---
title: "[자바 입문] 자바란"
excerpt: "김영한의 자바 입문 - 코로 시작하는 자바 첫걺음"

categories:
  - Java
tags:
  - [Java]

permalink: /java/test/

toc: true
toc_sticky: true

date: 2024-04-29
last_modified_at: 2024-04-29
---

## 🦥 본문
시험 기간에 자바에 대한 기초적인 부분이 항상 떨어진다고 생각했기에 , 시험이 끝나자마자!!바로!! 하는 못했고 시험끝나는 첫주부터 하기로 했다. 아마 아는것은 금방금방 건너 뛸듯하다.  
작성하고 싶은건 작성할듯?  
>ttps://www.inflearn.com/course/lecture?courseSlug=김영한의-자바-입문&unitId=194541&tab=curriculum  

### 자바란?
자바는 표준 스펙과 구현으로 나눌 수 있다.
- 자바 표준 스펙
  - 자바는 이렇게 만들어야 한다는 설계도이며, 문서이다.
  - 이 표준 스펙을 기반으로 여러 회사에서 실제 작동하는 자바를 만든다.
  - 자바 표준 스펙은 자바 커뮤니티 프로세스(JCP)을 통해 관리된다.
- 다양한 자바 구현
  - 여러 회사에서 자바 표준 스펙에 맞추어 실제 작동하는 자바 프로그램을 개발한다.
  - 각각 장단점이 있다. 예를 들어 Amazon Corretto AWS에 최적화 되어 있다.

  ### 컴파일과 실행
  자바 프로그램은 컴파일과 실행 단계를 거친다.
  - Hello.java와 같은 자바 소스 코드를 개발자가 작성한다.
  - 자바 컴파일러를 사용해서 소스 코드를 컴파일한다.
    - 자바가 제공하는 javac라는 프로그램을 사용한다.
    - `.java` -> `.class`파일이 생성된다.
    - 자바 소스 코드를 바이트 코드로 변환하며 자바 가상 머신에서 더 빠르게 실행될 수 있게 최적화하고 문법 오류도 검출한다.
  - 자바 프로그램을 실행한다.
    - 자바가 제공하는 java라는 프로그램을 사용한다.
    - 자바 가상 머신 (JVM)이 실행되면서 프로그램이 작동한다.

### 자바와 운영체제의 독립성
  - 일반적인 프로그램은 다른 운영체제에서 실행 할 수 없다.
  - 자바프로그램은 설치된 모든 os에서 실행할 수 있다.
  - 자바 개발자는 특정 OS에 맞추어 개발을 하지 않아도 된다. 자바 개발자는 자바에 맞추어 개발하면 된다. OS호환성 문제는 자바가 해결한다.

### 자바 개발과 운영환경 
  - 개발할 때 자바와 실행할 때 다른 자바를 사용할 수 있다.
  - 서버는 주로 리눅스를 사용.
  - 자바의 운영체제 독립성 덕분에 각각의 환경에 맞추어 자바를 설치하는 것이 가능하다.

### 스코프 존재 이유
- 비효율적인 메모리 사용 : 특정 블록에서 사용하는 변수를 그 블록에서 끝날때 바로바로 끝내주어야만 메모리 관리가 쉡다.
- 코드 복잡성 증가: 특정 코드 블록에서만 필요하고, 여기서만 사용하면 되므로 관리해야하는 변수가 줄게 된다. 하지만 블록이 끝난 다음에도 살아 있다면 계속 신경써야 하기 때문에 불편하다.


### 메서드 정의
```
public static int add(int a, int b){

}
제어자 반환타입 메서드 이름(매개변수 목록){
  메서드 본문
}
```
- 제어자 (Modifier) : pulic , static 과 같은 부분이다. 제어자는 뒤에서 설명한다. 지금은 항상 pulic, static, 키워드를 입력하자.
- 반환 타입(Return type) : 메서드가 실행 된 후 반환하는 데이터의 타입을 지정한다. 메서드가 값을 반환하지 않는 경우, 없다는 뜻의 void를 사용해야한다
- 메서드 이름 (Method Name) : 입력값으로 메서드 내부에서 사용할 수 있는 변수이다. 매게변수는 옵션이다. 입력갑이 필요 없는 메서드는 매개변수를 지정하지 않아도 된다.
- 메서드 본문 (Method Body) : 실제 메서드의 코드가 위치한다. 중괄호 `{}` 사이에 코드를 작성한다.


```
package method;

public class method2 {
    public static void main(String[] args) {
        printHeader();
        System.out.println("= 프로그램 실행중 = ");
        printFooter();
    }
    public static void printHeader(){
        System.out.println("= 프로그램을 시작합니다 =");
        return;
    }

    public static void printFooter(){
        System.out.println("= 프로그램을 종료합니다. =");
        return;
    }
}
````

- 매개변수가 없는 경우
  - 선언 : `public static void printHeader()` 와 같이 매개변수를 비워두고 정의하면 된다.
  - 호출 : `printHeadeer();`와 같이 인수를 비워두고 호출하면 된다.
- 반환 타입이 없는 경우
  - 선언 : `public static void printHeader()`와 같이 반환 타입을 void로 정의하면 된다.
  - 호출 : `printHedaer()`와 같이 반환타입이 없으므로 메서드만 호출하고 반환 값을 받지 않으면 된다.

### 반환타입
#### 반환타입이 있으면 반드시 값을 반환해야한다.
- 반환 타입이 있는 메서드는 반드시 return 을 사용해서 값을 반환해야한다. 이 부분은 특히 조건문과 함께 사용할 떄 주의 해야한다.
- return 문을 만나면 그 즉시 메서드를 빠져나간다.
