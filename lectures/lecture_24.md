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
