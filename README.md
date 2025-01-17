# 미션 - 자판기
##구현할 기능 목록

-프로그램 실행 -> Application.class
- [x] 메서드의 길이가 15라인을 넘어가지 않게
- [x] else 예약어 사용 X

### Controller
- VendingMachineController
- 자판기의 흐름을 제어한다.
- [x] 자판기의 입력, 출력을 수행한다.
- [x] 남은 금액이 상품의 최저 가격보다 적거나, 모든 상품이 소진된 경우 바로 잔돈을 돌려준다.
- [x] 잘못된 입력을 받으면 에러를 생성, 다시 입력을 받는다.
- [x] 구매가 더 이상 불가능 할 때까지 구매할 상품 명을 입력 받는다.

### View
- InputView
- 사용자의 입력을 받는 역할을 수행
- [x] 문자열로 사용자의 입력을 받는다.

- OutputView
- 게임 진행 중 출력을 하는 역할을 수행
- [x] 자판기가 보유한 동전 내역을 출력 한다.
- [x] 잔돈을 반환된 동전만 출력 한다.
- [x] 예외 상황 시 에러 문구를 출력 한다.

### Model
- Coin
- 게임 진행에 사용되는 VO Model

- HoldingCoins
- 자판기가 보유하고 있는 금액 입력에 대한 1급 컬렉션
- [x] 받은 금액이 양수인지 검증
- [x] 총 금액을 통해 동전을 무작위로 생성
- [x] 잔돈을 돌려줄 때는 현재 보유한 최소 개수의 동전으로 잔돈을 돌려 준다.

- VendingMachineMenu
- 자판기의 상품명, 가격, 수량 입력에 대한 VO
- [x] 메뉴 문자열이 입력 패턴을 따르는지 검증
- [x] Menus를 생성 후 넘겨주기

- Menu
- VendingMachineMenu를 파싱해서, 각 메뉴의 정보에 대한 VO
- [x] 메뉴 클래스는 상품명, 가격, 수량을 갖고 있다.
- [x] 상품 가격은 100원 이상, 10으로 나누어 떨어져야 한다.
- [x] 수량이 양수인지 검증
- [x] 메뉴 이름이 공백인지 검증

- Menus
- VendingMachine의 메뉴들을 관리하는 1급 컬렉션
- [x] Menu끼리 이름이 겹치는지 검증
- [x] 존재하는 Menu를 구입하는지 검증
- [x] Menu의 수량을 관리
- [x] 프로그램의 종료를 위해 상품의 최저 가격보다 적거나, 모든 상품이 소진된 경우를 관리
- [x] 주문 시 물건의 수량을 조절한다.

- InsertedMoney
- 투입 금액 입력에 대한 VO
- [x] 금액이 양수인지 검증
- 
## 🔍 진행방식

- 미션은 **기능 요구사항, 프로그래밍 요구사항, 과제 진행 요구사항** 세 가지로 구성되어 있다.
- 세 개의 요구사항을 만족하기 위해 노력한다. 특히 기능을 구현하기 전에 기능 목록을 만들고, 기능 단위로 커밋 하는 방식으로 진행한다.
- 기능 요구사항에 기재되지 않은 내용은 스스로 판단하여 구현한다.

## ✉️ 미션 제출 방법

- 미션 구현을 완료한 후 GitHub을 통해 제출해야 한다.
   - GitHub을 활용한 제출 방법은 [프리코스 과제 제출 문서](https://github.com/woowacourse/woowacourse-docs/tree/master/precourse) 를 참고해 제출한다.
- GitHub에 미션을 제출한 후 [우아한테크코스 지원 플랫폼](https://apply.techcourse.co.kr) 에 접속하여 프리코스 과제를 제출한다.
   - 자세한 방법은 [링크](https://github.com/woowacourse/woowacourse-docs/tree/master/precourse#제출-가이드) 를 참고한다.
   - **Pull Request만 보내고, 지원 플랫폼에서 과제를 제출하지 않으면 최종 제출하지 않은 것으로 처리되니 주의한다.**

## ✔️ 과제 제출 전 체크리스트 - 0점 방지

- 터미널에서 `java -version`을 실행해 자바 8인지 확인한다. 또는 Eclipse, IntelliJ IDEA와 같은 IDE의 자바 8로 실행하는지 확인한다.
- 터미널에서 맥 또는 리눅스 사용자의 경우 `./gradlew clean test`, 윈도우 사용자의 경우 `gradlew.bat clean test` 명령을 실행했을 때 모든 테스트가 아래와 같이 통과하는지 확인한다.

```
BUILD SUCCESSFUL in 0s
```

---

## 🚀 기능 요구사항

반환되는 동전이 최소한이 되는 자판기를 구현한다.

- 자판기가 보유하고 있는 금액으로 동전을 무작위로 생성한다.
   - 투입 금액으로는 동전을 생성하지 않는다.
- 잔돈을 돌려줄 때 현재 보유한 최소 개수의 동전으로 잔돈을 돌려준다.
- 지폐를 잔돈으로 반환하는 경우는 없다고 가정한다.
- 상품명, 가격, 수량을 입력하여 상품을 추가할 수 있다.
   - 상품 가격은 100원부터 시작하며, 10원으로 나누어떨어져야 한다.
- 사용자가 투입한 금액으로 상품을 구매할 수 있다.
- 남은 금액이 상품의 최저 가격보다 적거나, 모든 상품이 소진된 경우 바로 잔돈을 돌려준다.
- 잔돈을 반환할 수 없는 경우 잔돈으로 반환할 수 있는 금액만 반환한다.
   - 반환되지 않은 금액은 자판기에 남는다.
- 사용자가 잘못된 값을 입력할 경우 `IllegalArgumentException`를 발생시키고, "[ERROR]"로 시작하는 에러 메시지를 출력 후 해당 부분부터 다시 입력을 받는다.
- 아래의 프로그래밍 실행 결과 예시와 동일하게 입력과 출력이 이루어져야 한다.

### ✍🏻 입출력 요구사항

#### ⌨️ 입력

- 상품명, 가격, 수량은 쉼표로, 개별 상품은 대괄호([])로 묶어 세미콜론(;)으로 구분한다.

```
[콜라,1500,20];[사이다,1000,10]
```

#### 🖥 출력

- 자판기가 보유한 동전

```
500원 - 0개
100원 - 4개
50원 - 1개
10원 - 0개
```

- 잔돈은 반환된 동전만 출력한다.

```
100원 - 4개
50원 - 1개
```

- 예외 상황 시 에러 문구를 출력해야 한다. 단, 에러 문구는 [ERROR]로 시작해야 한다.

```
[ERROR] 금액은 숫자여야 합니다.
```

#### 💻 프로그래밍 실행 결과 예시

```
자판기가 보유하고 있는 금액을 입력해 주세요.
450

자판기가 보유한 동전
500원 - 0개
100원 - 4개
50원 - 1개
10원 - 0개

상품명과 가격, 수량을 입력해 주세요.
[콜라,1500,20];[사이다,1000,10]

투입 금액을 입력해 주세요.
3000

투입 금액: 3000원
구매할 상품명을 입력해 주세요.
콜라

투입 금액: 1500원
구매할 상품명을 입력해 주세요.
사이다

투입 금액: 500원
잔돈
100원 - 4개
50원 - 1개
```

---

## 🎱 프로그래밍 요구사항

- 프로그램을 실행하는 시작점은 `Application`의 `main()`이다.
- JDK 8 버전에서 실행 가능해야 한다. **JDK 8에서 정상 동작하지 않을 경우 0점 처리**한다.
- 자바 코드 컨벤션을 지키면서 프로그래밍한다.
   - https://naver.github.io/hackday-conventions-java
- indent(인덴트, 들여쓰기) depth를 3이 넘지 않도록 구현한다. 2까지만 허용한다.
   - 예를 들어 while문 안에 if문이 있으면 들여쓰기는 2이다.
   - 힌트: indent(인덴트, 들여쓰기) depth를 줄이는 좋은 방법은 함수(또는 메소드)를 분리하면 된다.
- 3항 연산자를 쓰지 않는다.
- 함수(또는 메소드)의 길이가 15라인을 넘어가지 않도록 구현한다.
   - 함수(또는 메소드)가 한 가지 일만 잘 하도록 구현한다.
- else 예약어를 쓰지 않는다.
   - 힌트: if 조건절에서 값을 return하는 방식으로 구현하면 else를 사용하지 않아도 된다.
   - else를 쓰지 말라고 하니 switch/case로 구현하는 경우가 있는데 switch/case도 허용하지 않는다.
- 프로그래밍 요구사항에서 별도로 변경 불가 안내가 없는 경우 파일 수정과 패키지 이동을 자유롭게 할 수 있다.

### 프로그래밍 요구사항 - Coin

- Coin 클래스를 활용해 구현해야 한다.
- 필드(인스턴스 변수)인 `amount`의 접근 제어자 private을 변경할 수 없다.

```java
public enum Coin {
    COIN_500(500),
    COIN_100(100),
    COIN_50(50),
    COIN_10(10);

    private final int amount;

    Coin(final int amount) {
        this.amount = amount;
    }

    // 추가 기능 구현
}
```

### 프로그래밍 요구사항 - Randoms, Console

- JDK에서 기본 제공하는 Random, Scanner API 대신 `camp.nextstep.edu.missionutils`에서 제공하는 `Randoms`, `Console` API를 활용해 구현해야 한다.
   - Random 값 추출은 `camp.nextstep.edu.missionutils.Randoms`의 `pickNumberInList()`를 활용한다.
   - 사용자가 입력하는 값은 `camp.nextstep.edu.missionutils.Console`의 `readLine()`을 활용한다.
- 프로그램 구현을 완료했을 때 `src/test/java` 디렉터리의 `ApplicationTest`에 있는 모든 테스트 케이스가 성공해야 한다. **테스트가 실패할 경우 0점 처리한다.**

---

## 📈 과제 진행 요구사항

- 미션은 [java-vendingmachine-precourse](https://github.com/woowacourse/java-vendingmachine-precourse) 저장소를 Fork/Clone해 시작한다.
- **기능을 구현하기 전에 java-vendingmachine-precourse/docs/README.md 파일에 구현할 기능 목록을 정리**해 추가한다.
- **Git의 커밋 단위는 앞 단계에서 README.md 파일에 정리한 기능 목록 단위**로 추가한다.
   - [AngularJS Commit Message Conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153) 참고해 commit log를 남긴다.
- 과제 진행 및 제출 방법은 [프리코스 과제 제출 문서](https://github.com/woowacourse/woowacourse-docs/tree/master/precourse) 를 참고한다.
