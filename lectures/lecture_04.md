# 라우터 

### 라우터 설치

```javascript
    npm i vue-router --save
    
    
    // package.json
    
    "dependencies" : { // 이 안은 실제 앱을 실행시키는데 필요한 비지니스로직, 동작 담당하는 배포할때도 필요한 라이브러리
        "vue": "^2.5.17"
        "vue-router": "^3.0.2"
    }
```
    
```javascript
### 라우터 사용 방법 1

    // main.js
    import VueRouter from 'vue-router';
    
    Vue.user(VueRouter);
    
    const router = new VueRouter({
        routes : [
            // 여기다 쭉쭉쭉
        ]
    })
    
    new Vue({
        render: h => h(App),
        router,
    }).$mount('#app')
```    
    
 이렇게 사용하면 main.js가 너무 코드가 길어짐  
 main.js는 프로젝트의 설정,플러그인, 라이브러리, 구조를 파악할 수 있는 청사진이 되어야 함.  
 
 
 ### 라우터 사용 방법 2 & redirect
 ```javascript
    // src/router/index.js  파일 생성
    import Vue from 'vue';
    import VueRouter from 'vue-router';
    import NewsView from '../views/NewsView.vue';
    import AskView from '../views/AskView.vue';
    
    Vue.use(VueRouter);
    
    export const router = new VueRouter({
        routes : [
            // 여기다 쭉쭉쭉
            {
              path: '', // url 주소
              component: '' //  url 주소로 갔을 때 표시될 컴포넌트, 페이지의 역할을 하는 컴포넌트
            },
            {
              path: '/',
              redirect: '/news'    // /이면 /news로 가라: 리다이렉트
            },
            {
              path: '/news',
              component: NewsView
            },
            
            {
              path: 'ask',
              component: AskView
            }
        ]
    });
    
    
    // src/views/NewsView.vue 생성
    // 이 폴더는 페이지 역할을 하는 파일을 모아두는 곳, views 안에서는 되도록 데이터 패치나 비지니스 로직을 
    <template>
        <div>news</div>
    </template>
    <script></script>
    <style></style>
    
    
    // main.js
    import Vue from 'vue';
    import App from './App.vue';
    import { router } from './router/index.js';
    
    new Vue({
        render: h => h(App),
        router,
    }).$mount('#app')
    
    
    // App.vue
    <template>
      <div id="app">
        // Strongly Recommended
        <ToolBar></ToolBar>
        // Essetial
        <tool-bar></tool-bar>
        <router-view></router-view>
      </div>
    </template>
    <script>
    import ToolBar from './components/ToolBar.vue'
    export default {
        components: {
            ToolBar,
        }
    }
    </script>
```   

 ### 라우터 링크 router-link   
```javascript  
    // componets/Toolbar.vue
    <template>
        <div>
            <router-link to="/news">News</router-link>  // 화면에서 a태그로 변환됨
            <router-link to="/ask">Ask</router-link>
            <router-link to="/jobs">News</router-link>
        </div>
    </template>
 ```  
    
    
 ```javascript   
 ### 라우터 폴더 작명 팁과 라우터 mode 안내      
 
    export const router = new VueRouter({
        mode: 'history', // 이렇게 쓰면 url에 #사라짐
        routes : [
            {
              path: '', // url 주소
              component: '' //  url 주소로 갔을 때 표시될 컴포넌트, 페이지의 역할을 하는 컴포넌트
            }
        ]
    });
 ```  
    
+ 라우터 폴더명을 routes로 하면 폴더 아이콘이 바뀜..
    
