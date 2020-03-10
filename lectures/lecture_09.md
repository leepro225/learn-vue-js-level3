# Vuex로 스토어 구현

### 구조의 차이
![11](./img/11.JPG)

- Vuex를 이용해 데이터를 스토어에 넣은 후 그걸 꺼내다 쓰는 구조를 만들어 보자.  



### 설치

    npm i vuex

    
### store구현

    // src/store/index.js 파일 만들고
    import Vue from 'vue';
    import Vuex from 'vuex';
    import { fetchNewsList } from '../api/index'

    Vue.use(Vuex); // vuex는 플러그인 형태로 제공되기 때문에 이렇게 사용해 준다..?

    export const store = new Vuex.Store({
        state: {
            news: []
        },
        mutations: {
            SET_NEWS(state, news) {
                state.news = news;
            }
        },
        actions: {
            FETCH_NEWS(context) {
                fetchNewsList()
                    .then(res => {
                        context.commit('SET_NEWS', res.data);
                    })
                    .catch(err => {
                        console.log(err);
                    });
            },
            FETCH_JOBS({commit}) {     // 이렇게 구조분해 할당으로 받는 것도 가능
                fetchJobsList()
                    .then(({data}) => {
                        commit('SET_JOBS', data);      // 이렇게 구조분해 할당으로 받는 것도 가능
                    })
                    .catch(err => {
                        console.log(err);
                    })
        }
        }
    });
    
    
    // main.js
    
    import Vue from 'vue';
    import App from './App.vue';
    import { router } from './routes/index.js';
    import { store } from './store/index.js';

    Vue.config.productionTip = false

    new Vue({
      render: h => h(App),
      router,
      store
    }).$mount("#app");
    
    
    // NewsView.vue
    <template>
    <div>
        <div v-for="user in this.$store.state.news" v-bind:key="user.id">{{ user.title }}</div>
       </div>
    </template>

    <script>

    export default {
        created() {
            this.$store.dispatch('FETCH_NEWS');
        }
    }
    </script>
    
    
    
 참고 : https://vuex.vuejs.org/


### 헬퍼함수 사용하기


    // AskView.vue
    <template>
        <div>
            <div v-for="item in fetchedAsk" v-bind:key="item.id">{{ item.title }}</div>
        </div>
    </template>

    <script>
    import { mapGetters } from 'vuex';
    export default {
        computed: {
            // #1방법 배열로
            ...mapGetters([
                'fetchedAsk'
            ]),
            // #1방법 객체로
            // ...mapGetters({
            //     ask : 'fetchedAsk'
            // })
            // #2방법
            // ...mapState({
            //     fetchedAsk: state => state.ask
            // }),
            // #3방법
            // ask() {
            //     return this.$store.state.ask;
            // }
        },
        created() {
            this.$store.dispatch('FETCH_ASK');
        }
    }
    </script>
    
    
    // store.js
    
    import Vue from 'vue';
    import Vuex from 'vuex';
    import { fetchNewsList, fetchJobsList, fetchAskList } from '../api/index'

    Vue.use(Vuex); // vuex는 플러그인 형태로 제공되기 때문에 이렇게 사용해 준다..?

    export const store = new Vuex.Store({
        state: {
            ask : []
        },
        mutations: {
            SET_ASK(state, ask) {
                state.ask = ask;
            }
        },
        getters: {
            fetchedAsk(state) {
                return state.ask;
            }
        },
        actions: {
            FETCH_ASK({commit}) {
                fetchAskList()
                    .then(({data}) => {
                        commit('SET_ASK', data);
                    })
                    .catch(err => {
                        console.log(err);
                    });
            }
        }
    });


스프레드연산자 참고 : https://joshua1988.github.io/es6-online-book/spread-operator.html
