# 키친포스

## 요구 사항

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

- [ ] StringNumber에 메시지를 보내자
  - 숫자들의 합을 구할 때 변환(`map`)하여 합산 하지말고, 객체에 메시지를 보내어 합산하는 책임을 위임하자
  - 변환하여 합산 하는 것은 getter 를 활용하는 것과 같으니 객체지향 생활 체조원칙 위반
  - stream 남용하여 생긴 일
- [ ] StringNumber 생성자에서 유효성 검증
  - 생성과 관련된 유효성 검증은 주 생성자에서 처리해야 중복을 피할 수 있다.
  - 생성자에서 하지 말아야 할 것은 비즈니스 로직
- [ ] 좋은 객체란
  - 😵‍💫
