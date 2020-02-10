# 리팩토링

### input쪽 코드

    <template>
      <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem">
        <span class="addContainer" v-on:click="addTodo">
          <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>
      </div>
    </template>

    <script>
    export default {
      data: function() {
        return {
          newTodoItem: ''
        }
      },
      methods: {
        addTodo: function() {
          if (this.newTodoItem !== '') {
            this.$emit('addItem', this.newTodoItem);
            this.clearInput();
          }
        },
        clearInput: function() {
          this.newTodoItem = '';
        }
      }
    }
    </script>
    
    
 ### list쪽 코드
    
    <template>
      <section>
        <ul>
          <li v-for="(todoItem, index) in propsdata" class="shadow" v-bind:key="todoItem.item">
            <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
                                             v-on:click="toggleComplete(todoItem, index)"></i>
            <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
            <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
              <i class="removeBtn fas fa-trash-alt"></i>
            </span>
          </li>
        </ul>
      </section>
    </template>

    <script>
    export default {
      props: ['propsdata'],
      methods: {
        removeTodo: function(todoItem, index) {
          this.$emit('removeItem', todoItem, index);
        },
        toggleComplete: function(todoItem, index) {
          this.$emit('toggleItem', todoItem, index); 
        }
      }
    }
    </script>
    
    
 ### footer쪽 코드
 
    <template>
      <div class="clearAllContainer">
        <span class="clearAllBtn" v-on:click="clearTodo">Clear All</span>
      </div>
    </template>

    <script>
    export default {
      methods: {
        clearTodo: function() {
          this.$emit('clearAll');
        }
      }
    }
    </script>
    
    
    
## 기존코드에서 리팩토링한 부분은 메서드들을 $emit을 이용해 한 곳으로 모았다는 것.


### app쪽 코드

    <template>
      <div id="app">
        <TodoHeader></TodoHeader>
        <TodoInput v-on:addItem="addOneItem"></TodoInput>
        <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
        <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
      </div>
    </template>

    <script>
    import TodoHeader from './components/TodoHeader.vue'
    import TodoInput from './components/TodoInput.vue'
    import TodoList from './components/TodoList.vue'
    import TodoFooter from './components/TodoFooter.vue'
    export default {
      data: function() {
        return {
          todoItems: []
        }
      },
      methods: {
        addOneItem: function(todoItem) {
          var obj = {completed: false, item: todoItem};
          localStorage.setItem(todoItem, JSON.stringify(obj));
          this.todoItems.push(obj);
        },
        removeOneItem: function(todoItem, index) {
          this.todoItems.splice(index, 1);
          localStorage.removeItem(todoItem.item);
        },
        toggleOneItem: function(todoItem, index) {
          todoItem.completed = !todoItem.completed;
          localStorage.removeItem(todoItem.item);
          localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        },
        clearAllItems: function() {
          this.todoItems = [];
          localStorage.clear();
        }
      },
      created: function() {
        if (localStorage.length > 0) {
          for (var i = 0; i < localStorage.length; i++) {
            if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
              this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            }
          }
        }
      },
      components: {
        TodoHeader: TodoHeader,
        TodoInput: TodoInput,
        TodoList: TodoList,
        TodoFooter: TodoFooter
      }  
    }
    </script>







