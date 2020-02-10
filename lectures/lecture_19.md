# mapMuations, mapActions

### mapMuations
 - Vuex에 선언한 mutations 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼
 
       // App.vue
       import { mapMuations } from 'vuex'

       methods() {
            ...mapMuations(['clickBtn'])
            authLogin() {},
            displayTable() {}
       }
 
       // store.js
       mutations: {
             clickBtn(state) {
                alert(state.msg);
             }
       }
 
       <button @click="clickBtn">popup message</button>


 ### mapActions
  - Vuex에 선언한 actions 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼
  
        // App.vue
        import { mapActions } from 'vuex'

        methods() { ...mapActions(['delayClickBtn'])}

        // store.js
        actions: {
              delayClickBtn(context) {
                    setTimeout(() => context.commit('clickBtn'), 2000);
              }
        }

        <button @click="delayClickBtn">delay popup message</button>

