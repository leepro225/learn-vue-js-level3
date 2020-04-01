# 스피너 컴포넌트

참고 주소 : https://github.com/joshua1988/vue-advanced/blob/12_spinner/vue-news/src/components/Spinner.vue


# 이벤트 버스란?
이벤트 버스란 빈 이벤트 객체를 통해 컴포넌트 간에 데이터를 전송하는 것
```javascript
      // src/utils/bus.js
      
      import Vue from 'vue';
      export const bus = new Vue();
      
      // 받아서 사용하는 쪽
      import { bux } from '../utils/bus.js;';
      
      
      
      // 이벤트 방출하는 쪽 src/views/VewsView.vue
      <template>
            <div>
                <list-item></list-item>
            </div>
      </template>
      <script>
      import ListItem from '../components/ListItem'
      import { bus } from '../utils/bus'

      export default {
          components: {
              ListItem
          },
          created() {
              bus.$emit('start:spinner');          // 스피너 시작하고
              this.$store.dispatch('FETCH_NEWS')   // 프라미스 객체인 res 돌려 받아 
                  .then(() => {
                   bus.$emit('end:spinner');       // 스피너 종료
                  });
          }
      }
      </script>
            
            
     // 이벤트 받는 곳 App.vue
     <template>
        <div id="app">
          <ToolBar></ToolBar>
          <transition name="fade">
          <router-view></router-view>
          </transition>
          <spinner :loading="loadingStatus"></spinner>
        </div>
      </template>

      <script>
      import ToolBar from './components/ToolBar'
      import Spinner from './components/Spinner'
      import { bus } from './utils/bus'


      export default {
        components: {
          ToolBar,
          Spinner
        },
        data() {
          return {
            loadingStatus: false
          }
        },
        methods: {
          startSpinner() {
            this.loadingStatus = true;
          },
          endSpinner() {
            this.loadingStatus = false;
          }
        },
        created() {
          bus.$on('start:spinner', this.startSpinner);
          bus.$on('end:spinner', this.endSpinner);
        },
        // 이벤트 버스는 이벤트 객체가 계속 쌓이기 때문에 컴포넌트의 역할이 끝난 후에 꼭 off 해주어야 한다.
        beforeDestroy() {
          bus.$off('start:spinner', this.startSpinner);
          bus.$off('end:spinner', this.endSpinner);
        }
      }
      </script>
  ```
