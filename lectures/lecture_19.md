# 라우터 네비게이션

### 문법


```javascript

  // routes/index.js

  import Vue from 'vue';
import VueRouter from 'vue-router';
import UserView from "../views/UserView.vue";
import ItemView from "../views/ItemView.vue";
import createListView from '../views/CreateListView.js';

Vue.use(VueRouter);

export const router = new VueRouter({
         mode: 'history',
         routes: [
           {
             path: '/',
             name: "news",
             redirect: '/news'
           },
           {
             path: "/news",
             name:"news",
             component: 'NewsView',
             beforeEnter: (to, from, next) => {
              store.dispatch('FETCH_LIST', to.name);
              .then(() => {
               // end spinner는 해당 컴포넌트 mounted로 옮기는 거 추천
               bus.$emit('end:spinner');
               next();
              })
              .catch((error) => {
               console.log(error);
              });
             }
           }
          ]
       });
