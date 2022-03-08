# 키친포스

## 요구 사항
식당에서 사용하는 주문관리 시스템을 구축한다.

- 상품
  - [ ] `이름`과 `가격`이 있다.
  - [ ] 등록된 상품들을 조회할 수 있다.
  - [ ] 이름에 비속어를 사용할 수 없다.
  - [ ] 가격을 변경할 수 있다.
  - [ ] 가격은 0원 이상이어야 한다.
  - [ ] 가격이 해당 상품을 포함하는 메뉴의 가격보다 크면 메뉴를 진열하지 않는다.
- 메뉴
  - [ ] `이름`, `가격`, `메뉴 그룹`, `진열 여부`, `1개 이상의 상품`이 있다.
  - [ ] 포함된 상품에는 수량이 있다.
  - [ ] 등록된 메뉴들을 조회할 수 있다.
  - [ ] 진열 여부를 변경할 수 있다.
  - [ ] 이름에 비속어를 사용할 수 없다.
  - [ ] 가격을 변경할 수 있다.
  - [ ] 가격은 0원 이상이어야 한다.
  - [ ] 가격은 메뉴에 포함된 상품별 총 금액(상품 가격 * 상품 수량)의 합보다 작아야 한다.
  - [ ] 하나의 메뉴 그룹에만 속한다.
  - [ ] 1개 이상의 상품을 포함한다.
  - [ ] 등록되지 않은 상품은 포함할 수 없다.
- 메뉴 그룹
  - [ ] `이름`이 있다.
  - [ ] 등록된 모든 메뉴 그룹을 조회할 수 있다.
- 식탁
  - [ ] `이름`, `손님 수`, `착석 여부`가 있다.
  - [ ] 식탁의 기본 상태는 0명의 손님이며 비어있다.
  - [ ] 모든 식탁을 조회할 수 있다.
  - [ ] 손님이 앉을 수 있다.
  - [ ] 손님이 앉으면 찬 상태다
  - [ ] 앉은 손님의 수를 변경할 수 있다.
  - [ ] 주문 완료된 식탁만 정리할 수 있다.
  - [ ] 정리된 식탁은 기본 상태가 된다.
- 주문
  - [ ] `주문 유형`, `주문 메뉴의 수량 및 가격`이 있다.
  - [ ] 주문 유형은 `배달`, `포장`, `식당 내 식사`다.
  - [ ] 배달 주문의 `상태`는 `대기`, `수락`, `조리 완료`, `배달 중`, `배달 완료`, `주문 완료` 순이다.  
  - [ ] 배달 주문은 `주소`가 있어야 한다.
  - [ ] 포장 또는 식당 내 식사 주문의 `상태`는 `대기`, `수락`, `조리 완료`, `주문 완료` 순이다.
  - [ ] 식당 내 식사는 빈 `식탁`이 있어야 한다.
  - [ ] `주문 시간`은 실시간으로 지정한다.
  - [ ] 등록된 메뉴가 진열되어야 한다.
  - [ ] 1개 이상의 메뉴를 주문해야 한다.
  - [ ] 지불한 금액이 주문한 메뉴의 총 금액과 일치해야 한다.
  - [ ] 주문의 기본 상태는 대기다.
  - 주문 수락
    - [ ] 대기 중인 주문만 수락할 수 있다.
    - [ ] 배달 주문은 배달 요청한다.
  - 주문 서빙
    - [ ] 수락된 주문만 서빙할 수 있다.
  - 배달 중
    - [ ] 배달 주문, 조리 완료 주문만 배달 시작할 수 있다.
  - 배달 완료
    - [ ] 배달 중인 주문만 주문 완료할 수 있다.
  - 주문 완료
    - [ ] 배달 완료된 배달 주문을 주문 완료할 수 있다.
    - [ ] 조리 완료된 포장 주문 또는 식당 내 식사 주문을 주문 완료할 수 있다.
    - [ ] 식당 내 식사 주문이 완료되면 식탁을 정리한다.
  - [ ] 모든 주문을 조회할 수 있다.
  

## 용어 사전

| 한글명 | 영문명 | 설명 |
| --- | --- | --- |
|  |  |  |

## 모델링

---

### 1단계 문자열 덧셈 계산기

- [x] 쉼표(,) 또는 콜론(:)을 구분자로 분리한 각 숫자의 합을 반환
  - [x] “” => 0
  - [x] "1,2" => 3
  - [x] "1,2,3" => 6
  - [x] “1,2:3” => 6
- [x] 쉼표(,) 또는 콜론(:)을 구분자로 분리
  - [x] "1,2" => "1", "2"
  - [x] “1,2:3” => "1", "2", "3"
  - [x] 빈 문자열 또는 null인 경우 빈 컬렉션 반환
- [x] 커스텀 구분자를 지정
  - [x] "//" 와 "\n" 사이의 문자
- [x] 문자열 계산기 예외 처리
  - [x] 숫자 이외의 값 
  - [x] 음수
- [x] 숫자 합산

### 1단계 피드백

- [x] StringNumber에 메시지를 보내자
  - 숫자들의 합을 구할 때 변환(`map`)하여 합산 하지말고, 객체에 메시지를 보내어 합산하는 책임을 위임하자
  - 변환하여 합산 하는 것은 getter 를 활용하는 것과 같으니 객체지향 생활 체조원칙 위반
  - stream 남용하여 생긴 일
- [x] StringNumber 생성자에서 유효성 검증
  - 생성과 관련된 유효성 검증은 주 생성자에서 처리해야 중복을 피할 수 있다.
  - 생성자에서 하지 말아야 할 것은 비즈니스 로직
- [ ] 좋은 객체란
  - [x] StringSplitter 이름 변경
    - End With -ER 은 안티패턴이다. 우선 이름부터 변경해보자. 
  - [x] StringNet 인터페이스 추출
  - [x] 기본 구분자로 분리
  - [x] 커스텀 구분자로 분리
  
### 2단계 피드백

- [x] `가격, 진열 여부를 변경할 수 있다.`
  - 여러 항목에 대한 공통 행위를 가지더라도 행위의 조건이 다르다면 분리하는 것이 요구사항을 명확하게 전달할 수 있다.
- [x] `식탁을 정리할 수 있다.`
  - 행위에 대한 조건이 누락됨.
- [ ] `식당 내 식사는 빈 식탁이 있어야 한다.`
  - 참조하는 도메인의 행위를 같이 고려해야 한다.
- [ ] `배달 주문, 조리 완료 주문만 배달 시작할 수 있다.`
  - 요구사항에서 사용되는 용어를 일치 시켜야 한다.
  - 같은 상태를 두고 서로 다른 용어를 사용하면 혼란을 일으킬 수 있다.
- [ ] 불필요한 공백 라인 제거
  - 공백 라인은 코드의 흐름(단락, 문단, 문맥)을 구분할 수 있게 사용해야 한다.
  - [참고자료](https://dsmoon.tistory.com/entry/%EC%A2%8B%EC%9D%80-%EC%BD%94%EB%93%9C-%ED%98%95%EC%8B%9D%EC%9D%B4%EB%9E%80)
- [ ] 결합도 낮추기
  - 클린코드 강의에서 배웠던 내용이다.
  - 결합도가 높으면 테스트가 어려워진다.
  - 애그리거트(?)에 대한 공부가 필요하다.
- [ ] 상수 객체
  - 상수 값을 활용한다면 상수 객체를 활용할 수 없는지 고민해봐야 한다.
  - ATDD 강의에서 비로그인 사용자를 표현하는 NonLoginMember를 사용했었다. 
