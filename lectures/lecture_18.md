# 헬퍼의 유연한 문법

### 헬퍼의 유연한 문법
 - Vuex에 선언한 속성을 그대로 컴포넌트에 연결하는 문법
 
       // 배열 리터럴
       ...mapMutations([
        'clickBtn', // 'clickBtn' : clickBtn
        'addNumber' // addNumber(인자)   인자 따로 안적어줘도 넘겨 받음
       ])
       
 - vuex에 선언한 속성을 컴포넌트의 특정 메서드에다가 연결하는 문법
       
       // 객체 리터럴
       ...mapMuations({
         popupMsg: 'clickbtn' // 컴포넌트 메서드 명 : Store 의 뮤테이션 명
       })
       
       
### 헬퍼 함수가 주는 간편함

    // Demo.vue
    <template>
     <div id="root">
      <p>{{ originPrice }}</p>
      <p>{{ doubledPrice }}</p>
      <p>{{ triplePrice }}</p>
     </div>
    </template>
    
    <script>
     import { mapGetters } from 'vuex';
     
     export default {
      computed: {
       ...mapGetters(['originPrice','doubledPrice','triplePrice']),  //이러케 하면 아래코드가 필요 없음
       
       // originPrice() {
       //  return this.$store.getters.originalPrice;
       // }
       // doubledPrice() {
       //  return this.$store.getters.doubledPrice;
       // }
       // triplePrice() {
       //  return this.$store.getters.triplePrice;
       // }
      }
     }
    </script>
    
    
    // demoStore.js
    import Vue from 'vue'
    import Vuex from 'vuex'
    
    Vue.use(Vuex);
    
    export const store = new Vuex.Store({
     state : {
       price : 100
     },
     getters: {
       originalPrice(state) {
        return state.price
       },
       
       doubledPrice(state) {
        return state.price * 2
       },
       
       triplePrice(state) {
        return state.price * 3
       }
     }
    });
