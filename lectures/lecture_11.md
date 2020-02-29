# 동적뷰 라우팅

###  문법

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
    
    
    
 ### 예시
 
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


참고 : https://router.vuejs.org/guide/essentials/dynamic-matching.html#reacting-to-params-changes
