# async & await 문법 소개

### 기본 문법
 - 함수의 앞에 async를 붙여주고 내부 로직 중 비동기 처리하고 싶은 함수 앞에 await를 붙인다. 이때 await가 붙은 함수는 Promise 객체를 반환한다.
 
       async function fetchData() {
        try {
          var list = await getUserList();
          console.log(list); // ['user1', 'user2', 'user3']
        } catch {
          // try 구문에서 실패시
        } finally {
          // try or catch가 끝난 후
        }
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
     
     
     
