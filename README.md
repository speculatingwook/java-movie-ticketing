# 미션 - 영화예매 시스템 구현

## 🔍 진행 방식

- 미션은 **기능 요구 사항, 프로그래밍 요구 사항, 과제 진행 요구 사항** 세 가지로 구성되어 있다.
- 세 개의 요구 사항을 만족하기 위해 노력한다. 특히 기능을 구현하기 전에 기능 목록을 만들고, 기능 단위로 커밋하는 방식으로 진행한다.
- 기능 요구 사항에 기재되지 않은 내용은 스스로 판단하여 구현한다.

## 🚨 과제 제출 전 체크 리스트 - 0점 방지

- 기능 구현을 모두 정상적으로 했더라도 **요구 사항에 명시된 출력값 형식을 지키지 않을 경우 0점으로 처리**한다.
- 기능 구현을 완료한 뒤 아래 가이드에 따라 테스트를 실행했을 때 모든 테스트가 성공하는지 확인한다.
- **테스트가 실패할 경우 0점으로 처리**되므로, 반드시 확인 후 제출한다.

### 테스트 실행 가이드

- 터미널에서 `java -version`을 실행하여 Java 버전이 17인지 확인한다.
  Eclipse 또는 IntelliJ IDEA와 같은 IDE에서 Java 17로 실행되는지 확인한다.
- 터미널에서 Mac 또는 Linux 사용자의 경우 `./gradlew clean test` 명령을 실행하고,
  Windows 사용자의 경우 `gradlew.bat clean test` 또는 `./gradlew.bat clean test` 명령을 실행할 때 모든 테스트가 아래와 같이 통과하는지 확인한다.
```text
BUILD SUCCESSFUL in 0s
```

---

## 🚀 기능 요구 사항

영화예매 기능을 구현해야 한다. 영화예매는 다음과 같은 규칙으로 진행된다.
### 영화정보
- 영화는 6:00 부터 24:00까지 2시간 간격으로 진행된다.
- 조조영화는 9:00 이전에 상영시작을 하는 것으로 전제한다.
```text
영화: 아바타
가격: 10,000원
할인 정책: 금액 할인 정책 (할인액: 800원)
할인 조건:
- 순번 조건: 조조 상영
- 순번 조건: 10회 상영
- 기간 조건: 월요일 10:00 ~ 12:00 사이 상영 시작
- 기간 조건: 목요일 18:00 ~ 21:00 사이 상영 시작

영화: 타이타닉
가격: 11,000원
할인 정책: 비율 할인 정책 (할인율: 10%)
할인 조건:
- 기간 조건: 화요일 14:00 ~ 17:00 사이 상영 시작
- 순번 조건: 2회 상영
- 기간 조건: 목요일 10:00 ~ 14:00 사이 상영 시작

영화: 스타워즈:깨어난 포스
가격: 10,000원
할인 정책: 없음
할인 조건: 없음
```
1. **영화 정보 관리**
  - 영화의 기본 정보(제목, 상영 시간, 가격 등)를 저장하고 조회할 수 있어야 한다.
  - 특정 영화의 상영 정보(상영 일자, 시간, 순번 등)를 저장하고 조회할 수 있어야 한다.
  - 순번은 하루 6:00부터 시작한 영화를 순서대로 1번부터 매긴다.

2. **예매 기능**
  - 사용자는 특정 영화의 상영 정보를 선택하여 예매할 수 있어야 한다.
  - 예매 시 인원 수를 입력받아야 한다.

3. **할인 규칙 적용**
  - 할인 조건(순서 조건, 기간 조건)과 할인 정책(금액 할인, 비율 할인)을 설정할 수 있어야 한다.
  - 예매 정보가 할인 조건을 만족하면 할인 정책에 따라 할인된 가격으로 예매할 수 있어야 한다.

세부 
  - 영화별로 하나의 할인 정책만 할당할 수 있다. 물론 할인 정책을 지정하지 않는 것도 가능하다.
  - 이와 달리 할인 조건은 다수의 할인 조건을 함께 지정할 수 있으며, 순서 조건과 기간 조건을 섞는 것도 가능하다

4. **예매 결과 출력**
  - 예매가 완료되면 예매 정보(제목, 상영 정보, 인원, 정가, 결제 금액)를 출력해야 한다.

### 입출력 요구 사항

#### 입력
- 프로그램 실행 시 영화 예매를 위한 사용자 입력을 받는다.
  - 예매할 영화 선택
  - 상영 정보 선택
  - 인원 수 입력

#### 출력
- 영화 목록 출력
- 선택한 영화의 상영 정보 출력
- 예매 완료 시 예매 정보 출력
  - 예매 정보: 제목, 상영 정보, 인원, 정가, 결제 금액

## 🎯 프로그래밍 요구 사항

- JDK 17 버전에서 실행 가능해야 한다. **JDK 17에서 정상적으로 동작하지 않을 경우 0점 처리한다.**
- 프로그램 실행의 시작점은 `Application`의 `main()`이다.
- `build.gradle` 파일을 변경할 수 없고, 외부 라이브러리를 사용하지 않는다.
- [Java 코드 컨벤션](https://github.com/woowacourse/woowacourse-docs/tree/master/styleguide/java) 가이드를 준수하며 프로그래밍한다.
- 프로그램 종료 시 `System.exit()`를 호출하지 않는다.
- 프로그램 구현이 완료되면 `ApplicationTest`의 모든 테스트가 성공해야 한다. **테스트가 실패할 경우 0점 처리한다.**
- 프로그래밍 요구 사항에서 달리 명시하지 않는 한 파일, 패키지 이름을 수정하거나 이동하지 않는다.
- indent(인덴트, 들여쓰기) depth를 3이 넘지 않도록 구현한다. 2까지만 허용한다.
  - 예를 들어 while문 안에 if문이 있으면 들여쓰기는 2이다.
  - 힌트: indent(인덴트, 들여쓰기) depth를 줄이는 좋은 방법은 함수(또는 메서드)를 분리하면 된다.
- 3항 연산자를 쓰지 않는다.
- 함수(또는 메서드)가 한 가지 일만 하도록 최대한 작게 만들어라.
- JUnit 5와 AssertJ를 이용하여 본인이 정리한 기능 목록이 정상 동작함을 테스트 코드로 확인한다.

### 추가된 요구 사항

- 함수(또는 메서드)의 길이가 15라인을 넘어가지 않도록 구현한다.
  - 함수(또는 메서드)가 한 가지 일만 잘 하도록 구현한다.
- else 예약어를 쓰지 않는다.
  - 힌트: if 조건절에서 값을 return하는 방식으로 구현하면 else를 사용하지 않아도 된다.
  - else를 쓰지 말라고 하니 switch/case로 구현하는 경우가 있는데 switch/case도 허용하지 않는다.
- 도메인 로직에 단위 테스트를 구현해야 한다. 단, UI(System.out, System.in, Scanner) 로직은 제외한다.
  - 핵심 로직을 구현하는 코드와 UI를 담당하는 로직을 분리해 구현한다.

---
