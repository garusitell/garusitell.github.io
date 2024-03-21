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

`하지만 뒤에 myAccount.setBalance(1000);` 이라는 코드를 못봤다면? 저걸 바꿀 이유를 모르기에 왜 바꿨지? 어디서 바꿧지? 할 수 있기때문에, 즉 왜 유지보수 입장 측면에서 바꿧냐가 문제가 되는것이다. 

Setter를 사용하면 객체의 속성이 갖는 값을 바꾼 이유를 알 수 없다.

### 다른 객체들로 책임이 분산된다.
Setter를 사용하면 해당 객체가 해야할일 (책임)을 다른객체가 해야할 수도 있다.
```java
@Service
public class AccountService {
    ...
    
    public void withdraw(long id, long amount) {
        Account account = accountRepository.findById(id).orElseThrow();
        long newBalance = account.getBalance() - amount;
        
        if (newBalance < 0) {
            throw new IllegalArgumentException("잔액이 부족합니다.");
        }
        
        account.setBalance(newBalance);
    }
    
    ...
}
```
원래라면 Account 객체에서 자신의 잔고를 관리하는 책임을 져야하지만 이 코드에서는 AccountService가 출금하려는 계좌의 잔고가 충분한지까지 확인하고 있다.  
Account가 책임을 다하지 않았기 때문에 AccountService 에서 Account가 할일을 대신 해주고 있는 것이다.

이렇게 어떤 객체가 해야할 일을 다른 객체가 해주고 있는데 객체의 구조가 변경된다 그 객체의 일을 대신 해주는 모든 코드를 수정해야한다.

### Getter 를 지양하는 경우
Setter를 지양하는 이유는 확실하게 와닿는다.

### Getter는 조회로 끝나지 않는 경우가 많다.
단순히 객체의 상태값이 뭔지 알고 싶어서 Getter를 사용하는 경우도 많지만, 많은 경우에 Getter로 상태값을 조회하면 그 값이 조건에 맞는지 확인하여 비즈니스로직을 수행하게 된다.
```java
public void withdraw(long id, long amount) {
    Account account = accountRepository.findById(id).orElseThrow();
    long newBalance = account.getBalance() - amount;
 
    if (newBalance < 0) {
        throw new IllegalArgumentException("잔액이 부족합니다.");
    }
 
    account.setBalance(newBalance);
}
```
여기서는 계좌에서 인출을 하기 위해 Account 객체에서 잔액을 조회해서 인출할 금액만큼 차감해보고 그 금액이 음수가 되는지 확인하고 있다.  
즉, 아래 과정을 수행하고 있는 것이다.  
1. 계좌의 잔액을 알려줘
2. 계좌의 금액 인출했을 때 잔액을 계산해보자
3. 금액을 인출했 때 잔액이 0보다 작은지 확인.

뭔가 이상하다. 그냥 인출할 금액을 전달해서 잔액이 충분한지만 물어보면 되는데 그걸 직접 확인해보는 셈이다.

### Getter를 통해 조건을 검사하면 변경에 취약하다
다음 예제 코드는 고객의 도시가스 이용 요금에 따라 고객 등급을 출력하는 예제이다.
```java
@Getter
class Customer {
    private long charge;
}
 
@Service
public class CustomerService {
    ...
    
    public void printMembershipGrade(Customer customer) {
        if (customer.getCharge() >= 100000) {
            System.out.println("Gold");
        } else if (customer.getCharge() >= 50000) {
            System.out.println("Silver");
        } else {
            System.out.println("Bronze");
        }
    }
    
    ...
}
```
코드 자체는 별 문제가 없어보인다. 그런데 요구사항이 변경되어 고객이 요금 대신 사용량과 단가만 갖게 된다면 어떻게 될까?
```java
@Getter
class Customer {
    private long usages;
    private long unitPrice;
}
```
이제 고객 객체에는 이용 요금에 대한 정보가 사라지고 사용량과 단가에 대한 정보가 담기게 되었다.  
하지만 CustomerService에서는 이러한 사실을 알지 못한다.  
더 이상 존재하지 않는 이용 요금을 조회하려고 할테니 당연히 컴파일 에러가 발생하게 된다.  
이 뿐만 아니라 기존에 charge의 값을 조회해서 사용하고 있던 코드를 모두 수정해야 한다. 역시 매우 끔찍한 일이다.  
이 역시 객체가 고객 등급을 결정하는 책임을 지지 않아서 발생한 문제이다.
### 그럼 Getter / Setter를 안 쓰고 어떻게 하라고?
지금까지 Getter와 Setter의 취약점에 대해 알아보았다.  
하지만 프로젝트를 진행하다 보면 객체의 상태를 바꿔야하거나 조회해야 하는 경우가 분명히 존재한다.  
그런데 Getter와 Setter를 쓰지 말라니..

아무런 대안도 없이 Getter와 Setter를 쓰지 말라고 하는 것은 아니다. 그 대안을 알아보자.

### Setter 대신 명확한 의도를 가진 메소드를 사용하라
앞서 봤던, 계좌에서 돈을 인출하는 예제를 다시 한 번 보자.
```java
@Setter
class Account {
    private long balance;
}
 
@Service
public class AccountService {
    ...
    
    public void withdraw(long id, long amount) {
        Account account = accountRepository.findById(id).orElseThrow();
        long newBalance = account.getBalance() - amount;
        
        if (newBalance < 0) {
            throw new IllegalArgumentException("잔액이 부족합니다.");
        }
        
        account.setBalance(newBalance);
    }
    
    ...
}
```
이 코드에서는 AccountService에서 계좌의 잔액이 충분한지 확인하고 계좌의 잔액을 변경하고 있다.  
이렇게 하지 말고 그냥 계좌에 출금할 금액을 전달해서 출금하라고 시키면 다음과 같은 코드가 된다.
```java

class Account {
    private long balance;
    
    public void withdraw(long amount) {
        if (amount > balance) {
            throw new IllegalArgumentException("잔액이 부족합니다.");
        }
        
        balance -= amount;
    }
}
 
@Service
public class AccountService {
    ...
    
    public void withdraw(long id, long amount) {
        Account account = accountRepository.findById(id).orElseThrow();
        account.withdraw(amount);
    }
    
    ...
}
```
코드도 간결해졌고 출금을 하겠다는 의도도 명확해졌다. 혹시나 출금 로직이 변경되더라도 Account 클래스의 withdraw()의 내용만 수정하면 된다. 다른 코드들은 Account의 withdraw()를 호출하고만 있어서 신경 쓸 필요가 없다.

 

이렇게 Setter 대신 명확한 의도를 가진 메소드를 사용했을 뿐인데 로직의 의도가 확실해졌고 계좌가 져야 할 책임이 분산되어 수정에 취약했던 문제도 해결되었다.

### Getter로 조건을 검사하지 말고 결과를 반환하게 하라
앞서, 도시 가스 이용 요금에 따라 고객 등급을 출력하는 예제에서는 고객의 정보가 바뀌면서 문제가 발생했다. 
이를 방지하기 위해 고객 객체에게 고객 등급을 반환하라고 시키면 아래와 같은 코드가 된다.

```java
class Customer {
    private long usages;
    private long unitPrice;
    
    public String calcMembershipGrade() {
        long charge = usages * unitPrice;
        
        if (charge >= 100000) {
            return "Gold";
        } else if (charge >= 50000) {
            return "Silver";
        } else {
            return "Bronze";
        }
    }
}
 
@Service
public class CustomerService {
    ...
    
    public void printMembershipGrade(Customer customer) {
        System.out.println(customer.calcMembershipGrade());
    }
    
    ...
}
```
이제 더 이상 CustomerService에서 고객의 등급을 출력하기 위해 고객의 상태를 알 필요가 없다. 그저 고객 객체에게 고객 등급을 계산해 달라고 시키기만 하면 되는 것이다.


> 출처 : https://colabear754.tistory.com/173(개발하는 곰돌이)
> 이 글을 가져가실려면 원본 주소에 여쭈어봐주세요!