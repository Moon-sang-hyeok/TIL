# Vue 06 Vue Router
## Routing
### Routing
- 네크워크에서 경로를 선택하는 프로세스
- 웹 애플리케이션에서 다른 페이지 간의 전환과 경로를 관리하는 기술

### SSR에서의 Routing
- SSR에서 routing은 서버 측에서 수행
- 서버가 사용자가 방문한 URL 경로를 기반으로 응답을 전송
- 링크를 클릭하면 브라우저는 서버로부터 HTML 응답을 수신하고 새 HTML로 전체 페이지를 다시 로드

### CSR에서의 Routing
- CSR에서 routing은 클라이언트 측에서 수행
- 클라이언트 측 JS가 새 데이터를 동적으로 가져와 전체 페이지를 다시 로드 하지 않음

### SPA에서 Routing이 없다면
- 유저가 URL을 통한 페이지의 변화를 감지할 수 없음
- 페이지가 무엇을 렌더링 중인지에 대한 상태를 알 수 없음
    - URL이 1개이기 때문에 새로 고침 시 처음 페이지로 되돌아감
    - 링크를 공유할 시 첫 페이지만 고융 가능
- 브라우저의 뒤로 가기 기능을 사용할 수 없음
- 페이지는 1개이지만, 주소에 따라 여러 컴포넌트를 새로 렌더링하여 마치 여러 페이지를 사용하는 것처럼 보이도록 해야 함

## Vue Router
### Vue Router
- Vue 공식 라우터

### Vue 프로젝트 구조 변화
1. App.vue 코드 변화
2. router 폴더 신규 생성
3. views 폴더 신규 생성

### RouterLink
- 페이지를 다시 로드 하지 않고 URL을 변경하여 URL 생성 및 관련 로직을 처리
- HTML의 a 태그를 렌더링
```
<RouterLink to="/">Home</RouterLink>
<RouterLink to="/about">About</RouterLink>
```

### RouterView
- RouterLink URL에 해당하는 컴포넌트를 표시
- 원하는 곳에 배치하여 컴포넌트를 레이아웃에 표시 할 수 있음

### router/index.js
- 라우팅에 관련된 정보 및 설정이 작성 되는 곳
- router에 URL과 컴포넌트를 매핑

### views
- RouterView 위치에 렌더링 할 컴포넌트를 배치
- 기존 components 폴더와 기능적으로 다른 것은 없으며 단순 분류의 의미로 구성됨

- 일반 컴포넌트와 구분하기 위해 컴포넌트 이름을 View로 끝나도록 작성하는 것을 권장

## Basic Routing
### 라우팅 기본
1. index.js에 라우터 관련 설정 작성(주소, 이름, 컴포넌트)
2. RouterLink의 'to' 속성으로 index.js에서 정의한 주소 값(path)을 사용
3. RouterLink 클릭 시 경로와 일치하는 컴포넌트가 RouterView에서 렌더링 됨

## Named Routes
### Named Routes
- 경로에 이름을 지정하는 라우팅
- name 속성 값에 경로에 대한 이름을 지정
- 경로에 연결하려면 RouterLink에 v-bind를 사용해 'to' props 객체로 전달

### Named Routes 장점
- 하드 코딩 된 URL을 사용하지 않아도 됨
- URL 입력 시 오타 방지

## Dynamic Route Matching
### Dynamic Route Matching
- URL의 일부를 변수로 사용하여 경로를 동적으로 매칭

### 매개변수를 사용한 동적 경로 매칭
- 주어진 패턴 경로를 동일한 컴포넌트에 매핑 해야 하는 경우 활용
- 예를 들어 모든 사용자의 ID를 활용하여 프로필 페이지 URL을 설계 한다면?
    - user/1
    - user/2
    - user/3
    - 일정한 패턴의 URL 작성을 반복해야 함

## Nested Routes
### Nested Routes
- 중첩된 라우팅
- 애플리케이션의 UI는 여러 레벨 깊이로 중첩된 컴포넌트로 구성되기도 함
- 이 경우 URL을 중첩된 컴포넌트의 구조에 따라 변경되도록 이 관계를 표현할 수 있음

1. 컴포넌트 생성
- componets 폴더에 UserProfile, UserPosts 컴포넌트 작성
2. 라우터 등록
- index.js에 두 컴포넌트를 import
- children 옵션
- children 옵션은 배열 형태로 필요한 만큼 중첩 관계를 표현할 수 있음
3. "children" 옵션을 사용해 중첩된 라우터에 컴포넌트를 등록
4. 두 컴포넌트에 대한 RouterLink 및 RoutterView 작성
5. Profile과 Posts 링크를 클릭해서 렌더링 결과 확인
6. 중첩된 Named Routes를 다룰때는 일반적으로 "하위 경로에만 이름을 지정"
    - 이렇게 하면 /user/:id로 이동했을 때 항상 중첩된 경로가 표시됨

7. UserHome 컴포넌트 생성

### 중첩된 라우팅
- 컴포넌트 간 부모-자식 관계 관점이 아닌 URL에서의 중첩된 관계를 표현하는 관점으로 바라보기

## Programmatic Navigation
### Programmatic Navigation
- RouterLink 대신 JS를 사용해 페이지를 이동하는 것

### 프로그래밍 방식 네비게이션
- 프로그래밍으로 URL 이동하기
- router의 인스턴스 메서드를 사용해 RouterLink로 a 태그를 만드는 것처럼 프로그래밍으로 네비게이션 관련 작업을 수행할 수 있음

### router의 메서드
1. 다른 위치로 이동하기
    - router.push()
2. 현재 위치 바뀍
    - router.replace()

### router.push()
- 다른 위치로 이동하기(Navigate to a different location)
- 다른 URL로 이동하는 메서드
- 새 항목을 history stack에 push하므로 사용자가 브라우저 뒤로 가기 버튼을 클릭하면 이전 URL로 이동할 수 있음
- RouterLink를 클릭했을 때 내부적으로 호출되는 메서드이므로 RouterLink를 클릭하는 것은 router.push()를 호출하는 것과 같음
- 선언적 표현 : RouterLink :to="..."
- 프로그래밍적 표현 : router.push(...)

### router.replace()
- 현재 위치 바꾸기(Replace current location)
- push 메서드와 달리 history stack에 새로운 항목을 push 하지 않고 다른 URL로 이동(=== 이동 전 URL로 뒤로 가기 불가)
- 선언적 표현 : RouterLink :to="..."
- 프로그래밍적 표현 : router.replace(...)

## Navigation Guard
### Navigation Guard
- Vue router를 통해 특정 URL에 접근할 때 다른 URL로 redirect를 하거나 취소하여 내비게이션을 보호 
- 라우트 전환 전/후 자동으로 실행되는 Hook

### Navigation Guard 종류
1. Globally (전역 가드)
    - 애플리케이션 전역에서 모든 라우트 전환에 적용되는 가드
2. Per-route (라우터 가드)
    - 특정 라우트에만 적용되는 가드
3. In-component (컴포넌트 가드)
    - 컴포넌트 내에서만 적용되는 가드

## Globally Guard
### Globally Guard
- 애플리케이션 전역에서 동작하는 가드
- 작성위치: index.js

### router.beforeEach()
- 다른 URL로 이동하기 직전에 실행되는 함수(Global Before Guards)
- 모든 가드는 2개의 인자를 받음
    - to : 이동 할 URL 정보가 담긴 Route 객체
    - from : 현재 URL 정보가 담긴 Route 객체

- 선택적으로 다음 값 중 하나를 반환
    1. false
        - 현재 내비게이션을 취소
        - 브라우저 URL이 변경된 경우(사용자가 수동으로 또는 뒤로가기 버튼을 통해)'from' 경로의 URL로 재설정
    2. Route Location
        - router.push()를 호출하는 것처럼 경로 위치를 전달하여 다른 위치로 redirect
        - return이 없다면 자동으로 'to' URL Route 객체로 이동

## Per-route Guard
### Per-route Gurad
- 특정 라우터에서만 동작하는 카드
- 작성위치: index.js의 각 routes
### router.beforeEnter()
- 특정 route에 진입했을 때만 실행되는 함수
- 단순히 URL의 매개변수나 쿼리 값이 변경될 때는 실행되지 않고, 다른 URL에서 탐색해 올 때만 실행됨

## In-component Guard
### In-component Guard
- 특정 컴포넌트 내에서만 동작하는 가드
- 작성위치: 각 컴포넌트의 script 내부

### In-component Guard 종류
- onBeforeRouteLeave()
    - 현재 라우트에서 다른 라우트로 이동하기 전에 실행
    - 사용자가 현재 페이지를 떠나는 동작에 대한 로직을 처리

- onBeforeRouteUPdate()
    - 이미 렌더링 된 컴포넌트가 같은 라우트 내에서 업데이트 되기 전에 실행
    - 라우트 업데이트 시 추가저인 로직을 처리


### Navigation Guard 정리
1. Globally(전역 가드)
    - 애플리케이션 전역에서 동작
    - 작성위치 : index.js
2. Per-route(라우터 가드)
    - 특정 route에서만 동작
    - 작성위치: index.js의 각 routes

3. In-component (컴포넌트 가드)
    - 특정 컴포넌트 내에서만 동작
    - 작성위치: 각 컴포넌트의 script

## Lazy Loading Routes
- Vue 애플리케이션 첫 빌드 시 해당 컴포넌트를 로드 하지 않고, "해당 경로를 처음으로 방문할 때 컴포넌트를 로드" 하는 것
- 앱을 빌드할 때 처음부터 모든 컴포넌트를 준비하면 컴포넌트의 크기에 딸 ㅏ페이지 로드 시간이 길어질 수 있기 때문