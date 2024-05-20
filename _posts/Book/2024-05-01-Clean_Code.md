---
title: "[관심있는 책] Clean Code"
excerpt: "꺠끗한 코드란 무엇인가?"

categories:
  - Book
tags:
  - [Book]

permalink: /book/CLEAN_CODEs/

toc: true
toc_sticky: true

date: 2024-05-01
last_modified_at: 2024-05-01
---

## 🦥 내용
### 장인정신.
- 첫째, 장인에게 필요한 원칙, 패턴 , 기법 , 경험 이라는 지식을 습득해야한다.
- 둘째 , 열심히 일하고 연습해 지식을 몸과 마음으로 체득해야한다.
깨끗한 코드를 작성하는 방법은 배우기 어렵다. 단순히 원칙과 패턴을 안다고 꺠끗한 코드가 나오지 않는다. 고생해야한다.  
이 책은 세 부분으로 나누어진다. 처음 몇장은 깨끗한 코드를 작성하는 원칙  
- 패턴 , 실기를 설명한다. 
둘째 부분은 더 어렵다. 각 사례 연구는 코드를 깨끗하게 고치는 , 즉 문제가 있는 코드를 문제가 더 적은 코드로 바꾸는 연습이다. 상세히 살펴보려면 집중력이 필요하다.
- 셋째 부분은 결말이다. 사례연구를 만들면서 수집하는 냄새와 후리스틱을 마지막 장에서 열거한다. 사례 연구에서 코드를 분석하고 정리하면서 우리 행위의 모든 이유를 휴리스틱이나 냄새로 정리했다. 여기서 휴리스틱 자체가 아니라 사례 연구에서 코드를 정리하면서 내린 각 결정과 휴리스틱 사이의 관걔가 중요하다.

### 코드가 존재하리라
궁극적으로 코드는요구사항을 표현하는 언어라는 사실을 명심한다. 요구사항에 더욱 가까운 언어를 만들 수도 있고, 요구사항에서 정형 구조를 뽑아내는 도구를 만들 수도 있다.  
하지만 어느 순간에는 정밀한 표현이 필요하다. 그 필요성을 없앨 방법은 없다. 그럼로 코드도 항상 존재하리라.

### 나쁜코드.
출시에 바빠 코드를 마구 짜거나, 기능을 추가할수록 코드는 엉망이 되어갔고, 결국은 감당이 불가능한 수준에 이르렀다. 회사가 망한 원인은 바로 나쁜 코드 탓이었다. 대충 짠 프로그램이 돌아간다는 사실에 안도감을 느끼며 그래도 안돌아가는 프로그램보다 돌아가는 쓰래기가 좋다고 스스로를 위로한 경험이 있다. 다시 돌아와 나중에 정리하겠다고 다짐했지만 르블랑의 법칙을 몰랐다. 그 떄는 다시 돌아욎 않는다.

### 나쁜 코드로 치르는 대가.
#### 나쁜 코드는 개발속도를 크게 떨어뜨린다.
코드를 고칠 때 마다 엉뚱한 곳에서 문제가 생간다. 간단한 변경은 없다.   
생산성을 증가시키려는 희망을 품고 프로젝트에 인력을 추가로 투입한다. 하지만 새 인력은 시스템 설계에 대한 조예가 깊지 않아, 설계의도에 맞는 변경과 설계 의도에 반하는 변경을 구분하지 못한다.  
게다가 새 인력과 팀은 생산성을 높여아 한다는 극심한 압력에 시달린다. 그래서 결국은 나쁜코드를 더 많이 양산한다.

#### 원대한 재 설계의 꿈
팀이 반기를 들며, 재설계를 요구한다. 새로운 팀은 기존 시스템 기능을 모두 제공하는 새 시스템은 물론 , 개발 중 기존 시스템에 가해지는 변경도 모두 따라 잡아야한다.

#### 태도
프로그래머도 마찬가지다, 나쁜 코드의 위험을 이해하지 못하는 관리자 말을 그대로 따르는 행동은 전문가 답지 못하다.

#### 원초적 난제
나쁜코드가 업무 속도를 늦춘다는 사실을 알지만. 그럼에도 기한을 맞출려면 나쁜 코드를 양산할 수 밖에 없다고 여긴다. 간단히 말해, 그들은 빨리 가려고 시간을 들이지 않는다. 진짜 전문가는 두 번째 부분이 틀렸다는 사실을 잘 안다. 빨리가는 유일한 방법은 , 언제나 코드를 최대한 꺠끗하게 유지하는 습관이라는 것을

#### 깨끗한 코드라는 예술?
깨끗한 코드를 작성하려면 '청결'이라는 힘겹게 습득한 감각을 활용해 자잘한 기법들을 적용하는 적제와 규율이 필요하다 . 그 열쇠는 '코드감각'이다. 

#### 깨끗한 코드란?

- 비야네 스트롭스트룹
>우아하고 효율적인 코드를 좋아한다. 논리가 간단해야 버그가 숨어들지 못하고, 의존성을 최대한 줄여야 유지보수가 쉬워진다. 오류는 명백한 전략에 의거해 철저히 처리한다. 성능을 최적으로 유지해야 사람들이 원칙 없는 최적화로 코드를 망치려는 유혹에 빠지지 않는다. 꺠끗한 코드는 한가지를 제대로 한다.

깨끗한 코드는 보는 사람에게 즐거움을 선사해야한다는 뜻이다.  
철처한 오류 처리도 언급하는데 , 세세한 사항까지 꼼꼼하게 신경쓰라는 말이다.  
나쁜코드는 너무 많은 일을 하려 애쓰다가 의도와 뒤섞이고 목적이 흐려진다. 꺠끗한 코드는 한가지에 집중하낟. 각 함수와 클래스와 모듈은 주변 상황에 현혹되거나 오염죄이 않은 채 한길만 걷는다.

- 그래디 부치
>깨끗한 코드는 단순하고 직접적이다. 꺠끗한 코드는 잘쓴 문장처럼 읽힌다. 꺠끗한 코드는 결코 설계자의 의도를 숨기지 않는다. 오히려 명쾌한 추상화와 단순한 제어문으로 가득하다.  

가독성을 강조한다. 깨끗한 코드가 잘 쓴 문장처럼 읽혀야 한다는 시각.  
코드는 추측이 아니라 사실에 기반해야 한다. 반드시 필요한 내용만 담아야 한다. 코드를 읽는 사람에게 프로그래머가 단호하다는 인상을 주어야한다.  

- 데이브 토마스
>깨끗한 코드는 작성자가 아닌 사람도 읽기 쉽고 고치기 쉽다. 단위 테스트 케이스와 인수 테스트 케이스가 존재한다. 깨끗한 코드에는 의미있는 이름이 붙는다. 특정 목적을 달성하는 방법은 (여러가지가 아니라) 하나만 제공한다. 의존성은 최소이며 각 의존성을 명확히 정의한다. API는 명확하며 최소로 줄였다. 언어에 따라 필요한 정보를 코드만으로 명확히 표현할 수 없기에 코드는 문학적으로 표현해야 마땅하다.   

데이브는 깨끗한 코드란 다른사람이 고치기 쉽다고 단언한다.  
꺠끗한 코드를 테스트 케이스와 연관짓는다. 테스트 케이스가 없는 코드는 꺠끗한 코드가 아니다.   
큰 코드보다 작은 코드에 가치를 둔다.  
인간이 읽기 좋은 코드를 작성하라는 말이다.

- 마이클 페더스
> 깨끗한 코드의 특징은 많지만 그 중에서 모두를 아우르는 특징이 하나 있다. 깨끗한 코드는 언제나 누군과 주의 깊게 짰다는 느낌을 준다. 고치려고 살펴봐도 딱히 손댈 곳이 없다 . 작성자가 이미 모든 사항을 고려헀으므로, 고칠 궁리를 하다보면 언제나 제자리로 돌아온다. 그리고는 누군가 남겨준 코드 , 누군가 주의 깊게 짜놓은 작품에 감사를 느낀다.  

깨끗한 코드는 주의 깊게 작성한 코드다.주의를 기울인 코드다.

- 론 제프리스
론은 스트레티직 에어 커맨드 사에서 포트란으로 프로그래밍을 시작한 이래 거의 모든 플랫폼에서 거의 모든 언어로 코드를 구현해왔다. 그러므로 그의 의견은 신중하게 고려할 가치가 있다.
> 켄트 백이 제한한 단순한 코드 규칙으로 구현을 시작한다.  
>1.모든 테스트를 통과한다  
>2.중복이 없다  
>3.시스템 내 모든 설계 아이디어를 표현한다.  
>4.클래스,메서드,함수등을 최대한 줄인다. 
<br>
<br> 
같은 작업을 여러 차례 반복한다면 코드가 아이디어를 제대로 표현하지 못한다는 증거다.  
> 표현력은 의미있는 이름을 포함한다.<br>객체가 여러 기능을 수행한다면 여러 객체로 나눈다.<br> 메서드가 여러 기능을 수행한다면 **메서드 추출 리팩터링 기법**을 적용해 기능을 명확히 기술하는 메서드 하나와 시능을 실제로 수행하는 메서드 여러개로 나눈다.<br><br>중복과 표현력만 신경써도 깨끗한 코드라는 목표에 성큼 다가선다. 지저분한 코드를 손볼 때 이 두가지만 고려해도 코드가 크게 나아진다.<br><br>프로그램이 아주 유사한 요소로 이뤄진다는 사실을 깨달았는데, ex) 어떤 집합에서 특정 항목을 찾아낼 필요.<br><br>이런 상황이 발생하면 추상메서드나 추상클래스를 만들어 실제 구현을 감싼다.<br><br> 간단하게 재빨리 구현했다가 나중에 필요할때 바꾸면 된다.<br><br>1.중복줄이기<br>2.표현력 높이기<br>3. 초반부터 간단한 추상화 고려하기  

`중복을 피하라, 한기능만 수행하라, 제대로 표현하라. 작게 추상화하라.`

- 워드 커닝햄
> 코드를 읽으면서 짐작했던 기능을 각 루틴이 그대로 수행한다면 깨끗한 코드라 불러도 되며 , 그 코드가 그 문제를 풀기 위한 언어처럼 보인다면 아름다운 코드라 불러도 된다.

깨끗한 코드는 읽으면서 놀랄일이 없어야 한다고 생각한다.모듈을 읽으면 다음에 벌어질 상황이 보인다. 

### 보이스카우트 규칙
- 잘 짠 코드가 전부는 아니며 , 시간이 지나도 언제나 깨끗하게 유지해야한다.  

`캠프장은 처음 왔을 때보다 더 깨끗하게 해놓고 떠나라`  
변수 이름 하나를 개선하고 , 조금 긴 함수 하나를 분할하고 , 약간의 중복을 제거하고 , 복잡한 if문 하나를 정리하면 충분하다.

#### 결론
예술에 대한 책과 마찬가지로 이 책 역시 세세한 정보로 가득하다. 코드도 많다. 좋은 코드도 소개하고 나쁜 코드도 소개한다. 나쁜 코드를 좋은 코드로 바꾸는 방법도 소개하며 ,다양한 경험적 교훈과 체계와 절차와 기법도 열거한다.'
<hr/>

### 의미있는 이름
#### 들어가면서
이름을 잘 짓는 간단한 규칙을 몇 가지 소개한다.

#### 의도를 분명히 밝혀라
변수나 함수 그리고 클래스 이름은 다음과 같은 굵직한 질문에 모두 답해야한다. 변수(혹은 함수나 클래스)의 존재 이유는? 존재 이유는? 수행 기능은? 사용 방법은? 따로 주석이 필요하다면 의도롤 분명히 드러내지 못했다는 말이다.ss
