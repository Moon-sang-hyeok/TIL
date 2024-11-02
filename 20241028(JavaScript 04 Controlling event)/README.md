# JavaScript 04 Controlling event

## 이벤트

### 웹에서의 이벤트

- 화면을 스크롤하는 것
- 버튼을 클릭했을 때 팝업 창이 출력되는 것
- 마우스 커서의 위치에 따라 드래그 앤 드롭하는 것
- 사용자의 키보드 입력 값에 따라 새로운 요소를 생성하는 것
- 웹에서의 모든 동작은 이벤트 발생과 함께 한다.

## event 객체

### event

- 무언가 일어났다는 신호, 사건
- 모든 DOM 요소는 이러한 event를 만들어 냄

### 'event' object

- DOM에서 이벤트가 발생했을 때 생성되는 객체
- 이벤트 종류
  - mouse, input, keyboard, touch ...

- DOM 요소에서 event가 발생하면, 해당 event는 연결된 이벤트 처리기(event handler)에 의해 처리 됨

## event handler

### event handler
- 특정 이벤트가 발생했을 때 실행되는 함수
- 사용자의 행동에 어떻게 반응할지를 JavaScript 코드로 표현한 것

### .addEventListener()
- 대표적인 이벤트 핸들러 중 하나
- 특정 이벤트를 DOM 요소가 수신할 때마다 콜백 함수를 호출

```
EventTarget.addEventListener(type, handler)
DOM 요소                    수신할 이벤트, 콜백 함수
```

"대상에 특정 Evnet가 발생하면, 지정한 이벤트를 받아 할 일을 등록한다."

### addEventListener의 인자
- type
  - 수신할 이벤트 이름
  - 문자열로 작성(ex. 'click')

- handler
  - 발생한 이벤트 객체를 수신하는 콜백 함수
  - 이벤트 핸들러는 자동으로 event 객체를 매개변수로 받음


### addEventListener 활용
- "버튼을 클릭하면 버튼 요소 출력하기"
- 버튼에 이벤트 처리기를 부착하여 클릭 이벤트가 발생하면 이벤트가 발생한 버튼정보를 출력