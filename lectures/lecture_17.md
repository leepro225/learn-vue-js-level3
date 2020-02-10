# mapState, mapGetters

### mapState
 - Vuex에 선언한 state 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼
 
       // App.vue
       import { mapState } from 'vuex'

       computed() {
            ...mapState(['num'])
            // num() { return this.$store.state.num; }
       }
 
       // store.js
       state : {
            num : 10
       }
 
       <!-- <p>{{ this.$store.state.num }}</p> -->
       <p>{{ this.num }}</p> // 이러케 가져다 쓸수 있음 헬퍼 함수로 받아왔으니


 ### mapGetters
  - Vuex에 선언한 getters 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼
  
        // App.vue
        import { mapGetters } from 'vuex'

        computed() { ...mapGetters(['reverseMessage'])}

        // store.js
        getters: {
              reverseMessage(state) {
                    return state.msg.split('').reverse().join('');
              }
        }

        <!-- <p>{{ this.$store.getters.reverseMessage }}</p>-->
        <p>{{ this.reverseMessage }}</p>

