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

