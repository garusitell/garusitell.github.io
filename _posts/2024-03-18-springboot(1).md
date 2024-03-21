---
title: "인프런 스프링 입문(7)"
excerpt: "회원관리 백엔드예제 - 비즈니스 요구사항 관리"

categories:
  - Springboot
tags:
  - [Springboot,스프링_입문]

permalink: /springboot/springboot_03_18_비즈니스요구사항관리/

toc: true
toc_sticky: true

date: 2024-03-18 20:00:00
last_modified_at: 2024-03-18 20:00:00
---

## 🦥 비즈니스 요구사항 관리

### 이제 회원관리 예제를 만드는 챕터이다.
>1. 비즈니스 요구사항  
>2. 회원 도메인과 리포지토리만들기
>3. 회원 리포지토리 케이스 작성
>4. 회원 서비스 개발
>5. 회원 서비스 테스트

### 비즈니스 요구사항 정리
  - 데이터 : 회원 ID,이름
  - 기능 : 회원등록 조회
  - 데이터 저장소가 설정되지않음(가상의 시나리오)
  
### 일반적인 웹 애플리케이션 구조
![image](https://github.com/garusitell/utterances/assets/45359953/42dcc993-7d25-4842-ac59-c6f5daeab46f)  

- 웹 컨트롤러 : 웹 MVC의 컨트롤러 역학
- 서비스 : 핵심 비즈니스 로직구현(EX, 회원등록 중복이 안된다는 로직)
- 리포지토리 : 데이터베이스에 접근,도메인 객체를 DB에 저장하고 관리

### 클래스 의존관계  
![image](https://github.com/garusitell/utterances/assets/45359953/023bca2b-b5d2-4c02-8422-3dafdaa379ab)
- 아직 데이터 저장소가 선정되지않아서, 우선 인터페이스로 구현
- 데이터 저장소는 RDB,NoSQL 등 다양한 저장소를 고민중인 상황
- 개발을 진행하기 위해 초기 개발단계에서는 구현체로 가벼운 메모리 기반의 데이터 저장소 사용


 7