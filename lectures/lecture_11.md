# 동적뷰 라우팅

###  문법
```javascript
    const User = {
      template: `<div>User {{ $route.params.id }}</div>`
    }

    const router = new VueRouter({
      routes: [
        { path: '/user/:id', component: User }
      ]
    })

    const app = new Vue({ router }).$mount('#app')
    
    <div id="app">
      <p>
        <router-link to="/user/foo">/user/foo</router-link>
        <router-link to="/user/bar">/user/bar</router-link>
      </p>
      <router-view></router-view>
    </div>
```    
    
    
 ### 예시
```javascript 
     // NewView.vue
     <template>
         <div>
             <p v-for="item in this.$store.state.news" v-bind:key="item.id">
                 <a :href="item.url">{{ item.title }}</a>   
                 <small style="color:#aaa5a5;">{{item.time_ago}} by 
                     <router-link v-bind:to="`/user/${item.user}`">{{item.user}}</router-link></small></p>
        </div>
     </template> 
     
     
     // routes/index.js
     import Vue from 'vue';
     import VueRouter from 'vue-router';
     import NewsView from "../views/NewsView.vue";

     Vue.use(VueRouter);

     export const router = new VueRouter({
              mode: 'history',
              routes: [
                {
                  path: '/',
                  redirect: '/news'
                },
                {
                  path: "/news",
                  component: NewsView
                },
                {
                  path: "/ask",
                  component: AskView
                },
                {
                  path: "/jobs",
                  component: JobsView
                },
                {
                  path: "/user/:id",
                  component: UserView
                },
               ]
            });

```
참고  
라우팅 https://router.vuejs.org/guide/essentials/dynamic-matching.html#reacting-to-params-changes  
v-html API문서 https://vuejs.org/v2/api/#v-html  
v-html과 데이터 바인딩 차이점 문서 https://vuejs.org/v2/guide/syntax.html#Raw-HTML


### 라우터 트랜지션

 화면 전환이 부드럽게 되게 하려궁.
 
 참고  
 라우터 트랜지션 문서 https://router.vuejs.org/guide/advanced/transitions.html#per-route-transition  
 뷰 트랜지션 문서 https://vuejs.org/v2/guide/transitions.html  
 
 #### 예시
```javascript 
    <!-- use a dynamic transition name -->
    <transition :name="transitionName">
      <router-view></router-view>
    </transition>
    
    .transitionName-enter-active, .transitionName-leave-active {
      transition: opacity .5s;
    }
    .transitionName-enter, .transitionName-leave-to /* .transitionName-leave-active below version 2.1.8 */ {
      opacity: 0;
    }
```   

