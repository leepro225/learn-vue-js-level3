# CLI로 생성한 프로젝트 배포하기

### npm run bulid

프로젝트 루트경로에서 npm run build를 터미널에 입력하면 dist 폴더가 생김.


### netlify

https://www.netlify.com/


### base 디렉토리 설정


### SPA 호스팅시에 서버에 추가해줘야 하는 설정

netlify 의 경우

    └public
      └ _redirects
      
      
      // _redirects
      
      /*      /index.html    200



### .env 파일로 환경변수 설정하기
- 설정한 변수들을 가지고 애플리케이션 로직에 활용할수도 있고, 웹팩으로 빌드를 할 때 변수의 내용을 반영할 수 있습니다.

        └프로젝트 폴더
            └ dist
            └ node_modules
            └ public
            └ src
            .env
            
            
         // .env
         
         VUE_APP_TEST = HELLO   // vue 파일에서 process.env.VUE_APP_TEST로 접근 가능
