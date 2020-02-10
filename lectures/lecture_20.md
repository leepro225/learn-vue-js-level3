# 프로젝트 구조화와 모듈화 방법

### 아래와 같은 store구조를 어떻게 모듈화 할 수 있을까?
 - Vuex에 선언한 state 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼
 
       // store.js
       import Vue from 'vue'
       import Vuex from 'vuex'
       
       export const store = new Vuex.Store({
         state: {},
         getters: {},
         mutations: {},
         actions: {}
       });

- 힌트! Vuex.Store({})의 속성을 모듈로 연결 



 ### 방법1) ES6의 Import & Export를 이용하여 속성별로 모듈화
 
     // store.js
     import Vue from 'vue'
     import Vuex from 'vuex'
     import * as getters from 'store/getters.js'
     import * as mutations from 'store/mutations.js'
     import * as actions from 'store/actions.js'
     
     export const store = new Vuex.Store({
       state: {},
       getters: getters,
       mutations: mutations,
       actions: actions
     });
     
     
     // mutations.js
     
     const removeItem = (state, payload) => { // 화살표 함수
      ... something logics
     };
     const addItem = (state, payload) => {
      ... something logics
     }
     const getItem = (state, payload) => {
      ... something logics
     }
     
     export {removeItem, addItem, getItem}
     
   ### 방법2) 앱이 비대해져 1개의 store로는 관리가 힘들때 modules 속성 사용
      
          // store.js
          import Vue from 'vue'
          import Vuex from 'vuex'
          import todo from 'modules/todo.js'
          
          export const store = new Vuex.Store({
            modules: {
              moduleA: todo, //모듈 명칭 : 모듈 파일명
              todo // todo: todo
            }; 
          });
          
          // todo.js
          const state = {
           // 속성
          }
          const getters = {}
          const mutations = {}
          const actions = {}
          
          export default {
           state,
           getters,
           mutations
          }
     
     
     
     
