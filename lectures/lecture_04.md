# 라우터 

### 라우터 설치

    npm i vue-router --save
    
    
    // package.json
    
    "dependencies" : { // 이 안은 실제 앱을 실행시키는데 필요한 비지니스로직, 동작 담당하는 배포할때도 필요한 라이브러리
        "vue": "^2.5.17"
        "vue-router": "^3.0.2"
    }
    
    
    
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
    
    
 이렇게 사용하면 main.js가 너무 코드가 길어짐  
 main.js는 프로젝트의 설정,플러그인, 라이브러리, 구조를 파악할 수 있는 청사진이 되어야 함.  
 
 
 ### 라우터 사용 방법 2
 
    // src/router/index.js  파일 생성
    import Vue from 'vue';
    import VueRouter from 'vue-router';
    
    Vue.user(VueRouter);
    
    const router = new VueRouter({
        routes : [
            // 여기다 쭉쭉쭉
            {
              path: '',
              component: ''
            }
        ]
    });
    
    
    
    
