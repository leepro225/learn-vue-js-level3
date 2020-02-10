# 설치하기

### npm

      npm i vuex --save
      
- 설치가 완료되면 package.json에 dependencies에 "vuex" : "버전"이 생김  

      
      
      
### vuex 파일 만들기(보통 store라고 함)

      - src
        └ store
            └ store.js
            
            
      
### store.js 파일 안, vuex 등록하기

      import Vue from 'vue' 
      import Vuex from 'vuex'
      
      Vue.use(Vuex);    // use는 vue의 플러그인, vuex를 전역으로 사용하겠다는 거
      
      export const store = new Vuex.Store({
            //
      )};
      
### main.js 파일 안, import하기

      import Vue from 'vue' 
      import App from './App.vue'
      import { store } from './store/store'

      new Vue({
         el : '#app',
         store,
         render : h => h(App)
      });


