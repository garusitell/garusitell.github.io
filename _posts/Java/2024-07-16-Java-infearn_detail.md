---
title: "[자바 입문]  기본형과 참조형 - 내가 헷갈린 예시문항"
excerpt: "김영한의 실전 자바 - 기본편"

categories:
  - Java
tags:
  - [Java]

permalink: /java/java_study_07_16_example/

toc: true
toc_sticky: true

date: 2024-07-16
last_modified_at: 2024-07-16
---

## 🦥 메서드에서 객체 반환
```java
public class Method2 {
    public static void main(String[] args) {
        Student student1 = createStudent("학생1",15,80);
        Student student2 = createStudent("학생2",16,90);

//        Student student2 = new Student(); //Shift + F6 를 누르면 같은 단어는 전부 같이 고칠 수 있다.
//        initStudent(student2,"학생2",16,80);

        System.out.println("이름 : " + student1.name + " 나이 : " + student1.age + " 성적 : " + student1.grade );
        System.out.println("이름 : " + student2.name + " 나이 : " + student2.age + " 성적 : " + student2.grade );

        printStudent(student1);
        printStudent(student2);
    }

    static Student createStudent (String name , int age , int grade){
        Student student = new Student();
        student.name = name;
        student.age = age;
        student.grade = grade;
        return student;

    }
    static void printStudent(Student student) {
        System.out.println("이름 : " + student.name + " 나이 : " + student.age + " 성적 : " + student.grade );

    }


}
```
- `createStudent()` 라는 메서드를 만들고 객체를 생성하는 부분도 이 메서드안에 함꼐 포함했으며 , 메서드 하나로 객체의 생성과 초기값 모두 처리한다.  
메서드안에서 객체를 생성했기 때문에 만들어진 객체를 메서드 밖에서 사용할 수 있게 돌려주어야 한다.  그래야 메서드 밖에서 이 사용할 수 있다. 메서드는 호출 결과를 반환 할 수 있으며 , 메서드의 반환 기능을 사용해서 만들어진 객체의 참조값을 메서드 밖에서 반환하면 된다.
![스크린샷 2024-07-16 오후 4 57 57](https://github.com/user-attachments/assets/d84090d7-d0f8-4802-828d-64c65b2ad981)

### NullPointerException
`NullPointerException`은 이름 그대로 `null`을 가리키다(Pointer)인데 , 이때 발생하는 예외(Exception)이다. `null`이라면 없다는 뜻으로 , 찾아갈 수 있는 객체(인스턴스)가 없다. `NullPointerException`은 이처럼 null에 .(dot)을 찍었을 때 발생한다.
```java
public class NullMain {
    public static void main(String[] args) {
        Data data = null;
        data.value = 10; //NullPointerException 예외 발생
        System.out.println("data = " + data.value);
    }
}
```
`data` 참조형 변수에는 `null`값이 들어가있다.
```java
Exception in thread "main" java.lang.NullPointerException: Cannot assign field "value" because "data" is null
	at ref.NullMain.main(NullMain.java:6)
```
결과적으로 `null` 값은 참조할 주소가 존재하지 않다는 뜻이다. 따라서 객체 인스턴스가 존재하지 않으므로 다음과 같이 `java.lang.NullPointerException` 이 발생하고 , 프로그램이 종료된다. 참고로 예외가 발생했기 떄문에 그 다음은 로직은 수행되지 않는다.
출처 : https://www.inflearn.com/course/김영한의-실전-자바-기본편/dashboard