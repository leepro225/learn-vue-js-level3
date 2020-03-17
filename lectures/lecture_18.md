# UX를 고려한 데이터 호출 시점


### 순서1.라우터 네비게이션 가드

- 훅보다 먼저 호출  
- 특정 URL로 접근하기 전의 동작을 정의하는 속성(함수)


### 순서2.컴포넌트 라이프 사이클 훅

- created : (컴포넌트가 생성)되자 마자 호출되는 로직


참고
- created 라이프 사이클 훅 API 문서 : https://vuejs.org/v2/api/#created  
- 네비게이션 가드 블로그 글 링크 : https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/  
- 네비게이션 가드 뷰 라우터 공식 문서 : https://router.vuejs.org/guide/advanced/navigation-guards.html#global-guards
