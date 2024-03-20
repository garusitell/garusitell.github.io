---
title: "Getter and Setter"
excerpt: "Getter and Setter의 사용법과 사용해야하는 이유"

categories:
  - Springboot
tags:
  - [Springboot,문법]

permalink: /springboot/getter_and_setter/

toc: true
toc_sticky: true

date: 2024-03-20
last_modified_at: 2024-03-20
---


### getter and setter 을 사용하는 이유
> 객체들의 데이터(필드)를 외부에서 직접적으로 접근하는것을 막아놓는다.  

필드들을 private 접근 제한자로 막아두고,  
각 필드의 Getter,Setter 로 접근하는 방식을 사용합니다.  
-> 객체의 무결성을 지키기 위함.  

ex> Man이라는 클래스에 weight(몸무게)라는 필드가 존재할때,  
weight는 0보다 작을 수 있으나.  

외부적으로 접근할 경우,  
weigh에 -100이라는 값을 줌으로서 객체의 무결성이 깨지는 일이 발생  

이를 방지하기 위해,  
필드를 private 로 만들어 외부의 접근을 제한한 후,  
Setter를 사용해 전달받은 값을 내부에서 가공해 필드에 넣어주는 방식을 사용함  

마찬가지로 필드값을 가져올때도,  
Getter를 사용해 본 필드의 값을 숨긴채  
내부에서 가공된 값을 꺼낼 수 있습니다.  

### getter and setter 을 되도록 사용하지 말아야하는 이유
우리는 자바를 `private` 를 통해 은닉하고, `public` 에서 접근을 허락함으로써 객체지향의 중요한 개념인 `캡슐화`를 만들게 된다.
  
하지만 getter과 setter 을 사용함으로써, 그 코드가 실행되어가는 와중에는 public이 아닌 다른 방향에서 그러한 접근을 허용하게 된다.  

그치만 시도 때도 없이 캡슐화한 객체에 진입하여 객체의 값을 바꿀려고 한다면 , 캡슐화의 의미가 퇴색될 우려가 많이 높다.

### Setter를 지양해야하는 경우
>Setter를 사용할때는 필요한 객체의 상태를 바꿀 수 있기 때문에 좋지만..  

**Setter 은 값을 바꾸는 이유를 말해주지 않는다.**
```java
class Account {
    private long balance;
    
    public Account(long balance) {
        this.balance = balance;
    }
    
    public void setBalance(long balance) {
        this.balance = balance;
    }
}
 
Account myAccount = new Account(500);
myAccount.setBalance(1000);
```
Account 클래스를 만들었다. 새로은 객체 myAccount에서 Account를 부여하고 500원을 이미 넣었다.

`하지만 뒤에 myAccount.setBalance(1000);` 이라는 코드를 못봤다면? 저걸 바꿀 이유를 모르기에 왜 바꿨지? 어디서 바꿧지? 할 수  


출저 : https://colabear754.tistory.com/173