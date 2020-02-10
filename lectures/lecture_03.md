# v-for 

### v-for를 이용해 리스트 뿌리기
    
    <template>
      <div>
        <ul>
          <li v-for="todoItem in todolist" v-bind:key="index">
            <span>{{ todoItem }}</span>
          </li>
        </ul>
      </div>
    </template>

    <script>
    export default {
        props: ['todolist'],
        data() {
                return {
        	        todoItems: []
            };
        },
        methods: {
            fetchTodoItems: function() {
                // 브라우저 저장소의 데이터를 불러오기
                for (var i = 0; i < localStorage.length; i++) {
            	    var item = localStorage.key(i);
           	        this.todoItems.push(item);
                }
                // 서버의 데이터 불러오기
                axios.get();
            }
        },
        // // 컴포넌트가 생성되자마자 실행되는 로직
        created: function() {
            this.fetchTodoItems();
        },
    };
    </script>
    <style>
    
    
    

### 삭제기능 구현하기
    
    <template>
      <div>
        <ul>
          <li v-for="(todoItem, index) in todolist"
                    v-bind:key="index">
            <span>{{ todoItem }}</span>
            <button 
              v-on:click="removeTodoItem(todoItem, index)">remove</button>
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
            removeTodoItem: function(todo, index) {
                // arr.splice('시작할 배열 인덱스', '갯수');
                this.todoItems.splice(index, 1);
                // 브라우저 저장소의 데이터 삭제
                localStorage.removeItem(todo);
            },
        }
    };
    </script>

    <style>
    </style>

    </style>
    

