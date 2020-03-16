# 하이오더 컴포넌트 (HOC)

### 정의
뷰의 하이 오더 컴포넌트는 리액트의 하이 오더 컴포넌트에서 기원된 것이다. 하이 오더 컴포넌트는 컴포넌트의 로직(코드)를 재사용하기 위한 고급 기술이다. 여기서 말하는 컴포넌트의 로직이란 뷰에서 인스턴스 옵션을 의미한다.


### 하이 오더 컴포넌트를 사용하기 전 코드
```javascript
<template>
<div>
    <list-item></list-item>
</div>
</template>
<script>
import ListItem from '../components/ListItem'
// import { bus } from '../utils/bus'

export default {
    components: {
        ListItem
    },
    created() {
        bus.$emit('start:spinner');
        this.$store.dispatch('FETCH_NEWS')   // 이 구간이 파일 마다 반복됨
            .then(() => {
                bus.$emit('end:spinner');
           });
    }
}
</script>
```



### 하이 오더 컴포넌트 적용

 ```javascript
 // views/CreateListView.js 파일 생성
 import ListView from './ListView.vue'
 import { bus } from '../utils/bus.js'

 export default function createListView(name) {
     return {
         // 재사용할 인스턴스(컴포넌트) 옵션들이 들어가는 자리
         name: name,
         created() {
             bus.$emit('start:spinner');
             this.$store.dispatch('FETCH_LIST', this.$route.name)
                 .then(() => {
                     bus.$emit('end:spinner');
                 })
                 .catch(e => console.log(e));
         },
         render(createElement) {
             return createElement(ListView);
         }
     }
 }
 ```
 
 ```javascript
 // route/index.js
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
             component: createListView('NewsView') // 동적으로 바인딩
           },
           {
             path: "/ask",
             name: "ask",
             component: createListView('AskView') // 동적으로 바인딩
           },
           {
             path: "/jobs",
             name: "jobs",
             component: createListView('JobsView') // 동적으로 바인딩
           },
           {
             path: "/item/:id",
             name:"item",
             component: ItemView
           },
           {
             path: "/user/:id",
             name: "user",
             component: UserView
           },
          ]
       });
 ```
       
       
 ```javascript
 // views/ListView.vue 빈 껍데기 생성
 <template>
    <div>
        <list-item></list-item>
    </div>
</template>
<script>
import ListItem from '../components/ListItem'
export default {
    components: {
        ListItem,
    }
}
</script>
```

```javascript 
// views/NewsView.vue   
<template>
<div>
    <list-item></list-item>
</div>
</template>
<script>
import ListItem from '../components/ListItem'
export default {
    components: {
        ListItem                 // 코드가 간단해짐
    }
}
</script>
```

```javascript
// api/index.js
function fetchList(pageName) {
    return axios.get(`${config.baseUrl}${pageName}/1.json`);
}

export {
    fetchList
}
```


```javascript
// store/actions.js
import {fetchList} from '../api/index'

export default {
   FETCH_LIST({commit}, pageName) {
            fetchList(pageName)
                .then(({ data }) => {
                    commit('SET_LIST', data);
                })
                .catch(e => console.log(e));
    }
}

```


```javascript
export default {
    // news: [],
    // jobs: [],
    ask: [],
    user: {},
    item: [],
    list: [] //추가
}
```

```javascript
// store/mutations.js
export default {
    SET_LIST(state, list) {
        state.list = list;
    }
}
```

![03.JPG]
