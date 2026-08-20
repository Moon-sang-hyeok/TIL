# 1강. Java 기초 — 변수, 자료형, 연산자

> **학습 환경**: IntelliJ IDEA 2024.3.2 / Amazon Corretto 17  
> **학습 목표**: Java 프로그램의 기본 구조를 이해하고 자료형, 연산자, 형변환을 설명할 수 있다.

## 1. 첫 Java 프로그램

```java
public class Main {
    public static void main(String[] args) {
        int age = 27;
        String name = "Kim";

        System.out.println(name);
        System.out.println(age);
    }
}
```

- `class Main`: 클래스를 정의한다.
- `main(String[] args)`: 일반적인 Java 프로그램의 실행 시작점이다.
- `System.out.println(...)`: 값을 출력하고 줄을 바꾼다.
- 대부분의 문장은 `;`로 끝나고 코드 블록은 `{ }`로 묶는다.
- Java는 **정적 타입 언어**다. 변수에 할당할 값의 종류를 타입으로 검사한다.

Python과 비교:

```python
age = 27
name = "Kim"
print(name)
print(age)
```

## 2. 자주 사용하는 자료형

| 타입 | 분류 | 예시 | 특징 |
|---|---|---|---|
| `int` | 기본형 | `10` | 정수 |
| `long` | 기본형 | `10L` | 더 넓은 정수 범위 |
| `double` | 기본형 | `3.14` | 부동소수점 실수 |
| `boolean` | 기본형 | `true` | 참/거짓 |
| `char` | 기본형 | `'A'` | 문자 한 개 |
| `String` | 참조형 | `"Java"` | 문자열 객체 |

```java
int count = 3;
double average = 87.5;
boolean passed = true;
char grade = 'A';
String subject = "Java";
```

> `String`은 기본형이 아니라 **참조형**이다. 기본형과 참조형의 차이는 6강에서 다룬다.

## 3. 산술 연산자

```java
int a = 10;
int b = 3;

System.out.println(a + b); // 13
System.out.println(a - b); // 7
System.out.println(a * b); // 30
System.out.println(a / b); // 3
System.out.println(a % b); // 1
```

- `/`: 정수끼리 나누면 정수 나눗셈이 되어 소수 부분이 **0을 향해 버려진다** (`-10 / 3` → `-3`).
- `%`: 나머지 연산자. 배수 판별 등에 유용하다.
- `+=`, `-=`, `++` 등은 값을 갱신하는 축약 연산자다.

## 4. 형변환: 언제 바꾸는지가 중요하다

```java
int a = 10;
int b = 3;

double first  = a / b;
double second = (double) a / b;
double third  = (double) (a / b);

System.out.println(first);  // 3.0
System.out.println(second); // 3.3333333333333335
System.out.println(third);  // 3.0
```

1. `a / b`: 먼저 정수 나눗셈을 수행하므로 `3`이 된다. 이후 `double` 변수에 저장하면서 `3.0`이 된다.
2. `(double) a / b`: 나누기 **전에** `a`를 `double`로 변환하므로 실수 나눗셈이 된다.
3. `(double) (a / b)`: 이미 정수 나눗셈으로 소수 부분이 사라진 뒤 형변환한다.

`double`은 2진 부동소수점 형식이므로 `1/3` 등의 값을 무한한 정밀도로 표현할 수 없다. 정확한 십진 금액 계산에는 상황에 따라 `BigDecimal` 등을 사용한다.

## 실습 및 정답

**문제**: 다음 코드의 출력값을 예상해 보자.

```java
int a = 10;
int b = 3;
System.out.println(a / b);
System.out.println(a % b);
System.out.println(a / 3.0);
```

**정답**

```text
3
1
3.3333333333333335
```

**핵심 정리**

- 정수끼리 나누면 정수 나눗셈이다.
- 나머지는 `%`로 구한다.
- 형변환은 **연산 전인지 후인지**에 따라 결과가 달라진다.

**다음 강의**: [2강 — 조건문과 논리 연산자](../02-conditions/README.md)
