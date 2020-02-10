# 스프레드 연산자와 헬퍼


### 헬퍼의 사용법
 - 헬퍼를 사용하고자 하는 vue 파일에서 아래와 같이 해당 헬퍼를 로딩

       // App.vue
       import { mapState } from 'vuex'
       import { mapGetters } from 'vuex'
       import { mapMutations } from 'vuex'
       import { mapActions } from 'vuex'

       export default {
             computed() { ...mapState(['num']), ...mapGetters(['countedNum'])},
             methods : { ...mapMutations(['clickBtn']), ...mapActions(['asyncClickBtn'])}
       }

this.num / this.conutedNum / this.clickBtn / this.asyncClickBtn 으로 컴포넌트 안에서 접근이 가능하다.  

### 뿌리는 연산자 ㅋㅋㅋObject Spread Operator
 - ...안에 여러개의 속성들이 뿌려져 있다 ?ㅋㅋㅋ  
 
       let josh = {
             field : 'web',
             language : 'js'
       };
       let developer = {
             nation : 'korea',
             field : josh.field
             lagnuage : josh.language   
        };
       
       console.log(developer); // { nation : 'korea', field : 'web', language : 'js' }
       
       // 이게 너무 기니까 ES6에서 나온 ...문법
       
       let developer = {
            nations : 'korea',
            ...josh
       };
       
       // 만약 이러케 해버리면??
       let developer = {
            nations : 'korea',
            josh
       }
       
       console.log(developer); // {nation : 'korea', josh {field : 'web', language : 'js'}}
      
     
