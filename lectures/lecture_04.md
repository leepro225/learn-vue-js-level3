# v-bind:class

### 토글 기능 구현

    <template>
      <div>
        <ul>
          <li v-for="(todoItem, index) in todolist"
                    v-bind:key="todoItem.item">
                    // 값이 true면 chekcBtnCompleted클래스 적용됨
            <i v-bind:class="{chekcBtnCompleted: todoItem.completed}"
               v-click="toggleComplete"></i>
            <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
            <button 
              v-on:click="removeTodoItem(todoItem, index)">remove</button>
            <button v-on:click="clearAll">clear All</button>
          </li>
        </ul>
      </div>
    </template>

    <script>
    export default {
        props: ['todolist'],
        data() {
            return {
                todoItems: [],
            };
        },
        methods: {
          toggleComplete : function(todoItem, index) {
                todoItem.completed = !todoItem.completed;   // 반대로 값을 바꿔주고
                localStorage.removeItem(todoItem);          // db에서 삭제하고
                localStorage.setItem(todoItem.item, JSON.stringify(todoItem);   // 변경된 값을 업데이트해주고
          },
          clearAll :  function() {
                localStorage.clear();   // 로컬스토리지 전부 비우는 함수
          }
        },
    };
    </script>

    <style>
    </style>
