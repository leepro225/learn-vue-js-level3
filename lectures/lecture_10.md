# 스토어 모듈화 하기

###  폴더구조

     - store
       - index.js
       - state.js
       - mutations.js
       - actions.js
       - getters.js
   
   
### 각 파일 내부

      // index.js
      
      import Vue from 'vue';
      import Vuex from 'vuex';
      import state from './state'
      import mutations from './mutations'
      import actions from './actions'
      import getters from './getters'

      Vue.use(Vuex); // vuex는 플러그인 형태로 제공되기 때문에 이렇게 사용해 준다..?

      export const store = new Vuex.Store({
          state,
          mutations,
          getters,
          actions 
      });
      
      // state.js
      
      export default {
          news: [],
          jobs: [],
          ask: []
      }
      
      
      // mutations.js
      
      export default {
           SET_NEWS(state, news) {
               state.news = news;
           },
           SET_JOBS(state, jobs) {
               state.jobs = jobs;
           },
           SET_ASK(state, ask) {
               state.ask = ask;
           }
       }
       
       // actions.js
       
       import { fetchNewsList, fetchJobsList, fetchAskList } from '../api/index'

       export default {
           FETCH_NEWS(context) {
               fetchNewsList()
                   .then(res => {
                       context.commit('SET_NEWS', res.data);
                   })
                   .catch(err => {
                       console.log(err);
                   });
           },
           FETCH_JOBS({ commit }) {
               fetchJobsList()
                   .then(({ data }) => {
                       commit('SET_JOBS', data);
                   })
                   .catch(err => {
                       console.log(err);
                   })
           },
           FETCH_ASK({ commit }) {
               fetchAskList()
                   .then(({ data }) => {
                       commit('SET_ASK', data);
                   })
                   .catch(err => {
                       console.log(err);
                   });
           }
       }
       
       // getters.js
       
       export default {
           fetchedAsk(state) {
               return state.ask;
           }
       }
       
       
       
      
      
    
    
