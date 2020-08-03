# async & await 문법 소개

### 기본 문법
 - 함수의 앞에 async를 붙여주고 내부 로직 중 비동기 처리하고 싶은 함수 앞에 await를 붙인다. 이때 await가 붙은 함수는 Promise 객체를 반환한다.
 
       async function fetchData() {
        var list = await getUserList();
        console.log(list); // ['user1', 'user2', 'user3']
       }
       
       function getUserList() {
        return new Promise(function (resolve, reject) {
          var userList = ['user1', 'user2', 'user3'];
          resolve(userList);
        });
       }


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
     
     
     
     
