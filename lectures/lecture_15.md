# 스피너 컴포넌트

참고 주소 : https://github.com/joshua1988/vue-advanced/blob/12_spinner/vue-news/src/components/Spinner.vue


# 이벤트 버스란?
이벤트 버스란 빈 이벤트 객체를 통해 컴포넌트 간에 데이터를 전송하는 것

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
                    bus.$emit('start:spinner');
                    this.$store.dispatch('FETCH_NEWS');
                    bus.$emit('end:spinner');
                }
            }
            </script>
