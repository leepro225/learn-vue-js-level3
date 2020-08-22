# Component Design Patterns 

### 컴포넌트 디자인 패턴 소개

1. Common - 기본적인 컴포넌트 등록과 컴포넌트 통신
2. Slot - 마크업 확장이 가능한 컴포넌트
3. Controlled - 결합력이 높은 컴포넌트
4. Renderless - 데이터 처리 컴포넌트

### 1. Common Approach
- 기본적인 컴포넌트 설계 방식
- 컨테이터 컴포넌트와 프레젠테이션 컴포넌트로 구성

        // 폴더 구조
        components
          └ AppContent.vue
          └ AppHeader.vue
        App.uve
        
        
        //  AppContent.vue
        
        <template>
          <div>
              <ul>
                <li v-for="item in items"> {{ item }} </li>
              </ul>
              <button @click="$emit('renew')"></button>
          </div>
        </template>
        <script>
          export default {
            props: {
              items: {                             // pros validation 참고
                type: Array,                       // props를 넘길때 항상 타입이 배열이어야함
                required: true                              
              }
            }
          }
        </script>
        
        
        // AppHeader.vue
        
        <template>
           <header>
              <h1>{{ title }}</h1>     
           </header>
        </template>
        <script>
        export default {
           props: ['title'],
           props: {
              title: String
           }
        }
        </script>
        
        // App.vue
        
        <template>
          <div>
            <app-header :title="appTitle"></app-header>
            <app-content :items="items" @renew="renewItems"></app-content>
          </div>
        </template>
        <script>
        import AppHeader from './components/AppHeader.vue'
        import AppContent from './components/AppContent.vue'
        
        export default {
          components: {
            AppHeader,
            AppContent
          },
          data() {
            return {
              appTitle: 'Common Approach',
              items: [10, 20, 30]
            }
          },
          methods: {
            renewItems() {
              this.items = [40, 50, 60];
            }
          }
        }
        </script>
        
        
### 2. Slots
- 마크업 확장이 가능한 컴포넌트

        // 폴더 구조
        └ App.vue
        └ item.vue
        
        // App.vue
        <template>
            <div>
               <ul>
                  <item>
                     아이템 1
                  </item>
                  <item>
                     아이템 2 <button>Click Me</button> // 이렇게 다양하게 마크업을 변형 가능
                  </item>
                  <item>
                     <div>
                       아이템 3
                     </div>
                     <img src="./assets/endgame.png">
                  </item>
                  <item>
                     <div style="color:blue;">아이템 4</div>
                  </item>
               </ul>
            </div>
        </template>
        <script>
        import Item from './Item.vue'
        
        export default {
           components: {
              Item
           }
        }
        </script>
        
        
        // Item.vue
        
        <template>
          <li>
            <slot>
            <!-- 등록하는 곳에서 정의할 화면 영역-->
               {{ item }}
            </slot>
          </li>
        </template>
              
