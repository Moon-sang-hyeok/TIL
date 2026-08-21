# 2강. 조건문과 논리 연산자

> **학습 목표**: 조건문의 실행 순서와 `&&`, `||`의 단락 평가를 이해한다.

## 1. if / else if / else

```java
int score = 85;

if (score >= 90) {
    System.out.println("A");
} else if (score >= 80) {
    System.out.println("B");
} else {
    System.out.println("C");
}
// B
```

`if → else if → else` 순서대로 평가하며, **처음 참인 분기 하나**만 실행한다. 여러 분기를 실행하려면 독립된 `if`문을 사용해야 한다.

```java
int score = 95;
if (score >= 60) {
    System.out.println("합격");
} else if (score >= 90) {
    System.out.println("우수");
}
// 합격: 이미 첫 번째 조건이 true이기 때문
```

Java에서는 조건식이 반드시 `boolean`이어야 한다. `if (1)`은 사용할 수 없다.

## 2. 비교 연산자와 논리 연산자

| Java | 의미 | Python과 비교 |
|---|---|---|
| `==`, `!=` | 같음, 다름 | 숫자/기본형 값 비교 |
| `>`, `<`, `>=`, `<=` | 대소 비교 | Python과 유사 |
| `&&` | AND | `and` |
| `||` | OR | `or` |
| `!` | NOT | `not` |

**주의**: Java에서는 Python의 `and`, `or` 키워드 대신 `&&`, `||`를 사용한다.

## 3. 단락 평가 (Short-circuit evaluation)

- `A && B`: `A`가 거짓이면 `B`를 검사하지 않는다.
- `A || B`: `A`가 참이면 `B`를 검사하지 않는다.

```java
int a = 10;
int b = 0;

if (b != 0 && a / b > 2) {
    System.out.println("A");
} else {
    System.out.println("B");
}
// B
```

`b != 0`이 `false`이기 때문에 `a / b`는 실행되지 않는다. 따라서 0으로 나누는 오류도 발생하지 않는다.

실무 예제:

```java
String name = null;
if (name != null && name.length() > 3) {
    System.out.println("이름이 너무 깁니다.");
}
```

먼저 `null` 여부를 확인해 뒤의 메서드 호출에서 `NullPointerException`이 발생하는 것을 방지한다.

> `&`와 `|`도 boolean 연산에 사용할 수 있지만 **양쪽을 모두 평가**한다. 단락 평가가 필요한 조건식에서는 주로 `&&`, `||`를 사용한다.

## 실습 및 정답

**문제 A**

```java
int a = 10;
int b = 5;
if (a > 5 && b > 10) {
    System.out.println("A");
} else if (a > 5 || b > 10) {
    System.out.println("B");
} else {
    System.out.println("C");
}
```

**정답**: `B`. 첫 번째는 `true && false` → `false`; 두 번째는 `true || false` → `true`다.

**문제 B**

```java
int x = 10;
int y = 0;
if (y != 0 && x / y > 2) {
    System.out.println("A");
} else {
    System.out.println("B");
}
```

**정답**: `B`. `&&`의 오른쪽을 평가하지 않는다.

**이전에 헷갈린 부분**

- `&&`가 false일 때 `else`로 이동한다는 점
- `||`는 하나라도 true면 true라는 점
- Python의 `and`와 Java의 `&&`를 혼동하지 않기

**다음 강의**: [3강 — 반복문](../03-loops/README.md)
