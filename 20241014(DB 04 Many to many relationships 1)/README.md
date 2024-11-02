# DB 04 Many to many relationships 1

## Many to many relationships N:M or M:N

- 한 테이블의 0개 이상의 레코드가 다른 테이블의 0개 이상의 레코드와 관련된 경우
- 양쪽 모두에서 N:1 관계를 가짐

## N:1의 한계 상황

- 1번 환자(carol)가 두 의사 모두에게 진료를 받고자 한다면 환자 테이블에 1번 환자 데이터가 중복으로 입력

hospitals_doctor

|id|name|
|--|---|
|1|allie|
|2|barbie|

hosptials_patient
|id|name|docotr_id|
|--|---|----|
|1|carol|1|
|2|duke|2|
|3|carol|2|
|4|carol|1,2|

- 외래 키 컬럼에 '1,2'형태로 저장하는 것은 DB 타입 문제로 불가능

## 중개 모델
1. 예약 모델 생성
    - 환자 모델의 외래 키를 삭제하고 별도의 예약 모델을 새로 생성
    - 예약 모델은 의사와 환자에 각각 N:1 관계를 가짐

## ManyToManyField()
M:N 관계 설정 모델 필드

## 'through' argument
중개 테이블에 '추가 데이터'를 사용해 M:N 관계를 형성하려는 경우에 사용

- Reservation Class 재작성 및 through 설정

- 예약 생성 방법 1
    - Reservation class를 통한 예약 생성

    ```
    reservation1 = Reservation(doctor=doctor1, ptient=patient1, symptom='headache')
    ```
- 예약 생성 방법 2
    - Patient 또는 Doctor의 인스턴스를 통한 에약 생성 (through_defaults)
    ```
    patient2.doctors.add(doctor1, through_defaults={'symptom':'flu'})
    ```

- 생성과 마찬가지로 의사와 환자 모두 각각 예약 삭제 가능

```
doctor1.patient_set.remove(patient1)

patient2.doctors.remove(doctor1)

```

## M:N 관계 주요 사항
- M:N 관계로 맺어진 두 테이블에는 물리적인 변화가 없음
- ManyToManyField는 중개 테이블을 자동으로 생성
- ManyToManyField는 M:N 관계를 맺는 두 모델 어디에 위치해도 상관 없음
    - 대신 필드 작성 위치에 따라 참조와 역참조 방향을 주의할 것
- N:1은 완전한 종속의 관계였지만 M:N은 종속적인 관계가 아니며 '의사에게 진찰받는 환자 & 환자를 진찰하는 의사' 이렇게 2가지 형태 모두 표현 가능

## ManyToManyField(to, **options)
M:N 관계 설정 시 사용하는 모델 필드

ManyToManyField 특징
-
- 양방향 관계
    - 어느 모델에서든 관련 객체에 접근할 수 있음
- 중복 방지
    - 동일한 관계는 한 번만 저장됨


ManyToManyField의 대표 인자 3가지
-
1. related_name
2. symmetrical
3. through