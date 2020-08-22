# Component Design patterns(2)

### 3. Controlled Component 
- Input 박스를 다룰때 생기는 문제점
- 이때 뜨는 에러 : [Vue warn] Avoid mutating a prop directly since the value will be overwitten whenever the parent component re-render.
- 자식이 직접 props를 바꾸면 안된다는 뜻

      // input 박스를 다룰때 생기는 문제점

      // 부모
      <template>
        <check-box checked="checked"></check-box>
      </template>
      <script>
      import CheckBox from './components/CheckBox.vue';
      
      export default {
        components: {
          CheckBox
        },
        data() {
          return {
            checked: false
          }
        }
      }
      </script>
      
      // 자식
      <template>
        <input type="checkbox" v-model="checked">
      </template>
      <script>
      export default {
        props: ['checked']
      }
      </script>
      
      
- 해결 방법 : 이렇게 하면 자식이 props를 바로 바꾸는게 아니라 이벤트를 방출하는 것이므로 에러가 안나고, 상위에서 데이터를 컨트롤할 수 있게 됨.

      // 부모
      <template>
         <check-box v-model="checked"></check-box>
      </template>
      <script>
      import CheckBox from './components/CheckBox';
      
      export default {
        components: {
           CheckBox
        },
        date() {
           return {
             checked: false
           }
        }
      }  
      </script>
      
      // 자식
      <template>
         <input type="checkbox" :value="value" @click="toggleCheckBox">
      </template>
      <script>
      export default {
        // @input 이벤트로 부모에게 방출
        // :value 값 내려 받기
        props: ['value'], //false
        methods: {
           toggleCheckBox() {
               this.$emit('input', !this.value);
           }
        }
      }
      </script>
      
 
 ### 그냥
 - 여기서 h는 highper script
 
            new Vue({
                  reder: h => h(app), // es6 이게 되는 과정
                  // 1
                  render: function(createElment) {
                        return createElement(App);
                  },
                  // 2
                  render: function(h) {
                        return h(App);
                  },
                  // 3
                  render: (h) => {
                                    h(app);
                                 }
            }).$mount('#app');

      
