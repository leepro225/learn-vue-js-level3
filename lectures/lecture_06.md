# Modal Component 활용하기

### 활용을 해봅시당

https://vuejs.org/v2/examples/modal.html 
접속해서 html/css/js 긁어와~~


### slot

slot을 이용해 특정 컴포넌트의 특정 UI를 재정의 하여 재사용할 수 있다.

#### 팝업 띄울 컴포넌트

    <template>
      <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
          <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>

        <Modal v-if="showModal" @close="showModal = false">     // 사용할 컴포넌트에 모달 컴포넌트 등록
          <h3 slot="header">
            경고  // 여기다가 내가 쓰고 싶은거 재정의
            <i class="closeModalBtn fa fa-times" 
              aria-hidden="true" 
              @click="showModal = false">
            </i>
          </h3>
          <p slot="body">할 일을 입력하세요.</p>   // 여기다가 내가 쓰고 싶은거 재정의
        </Modal>
      </div>
    </template>

    <script>
    import Modal from './common/Modal.vue'
    export default {
      data: function() {
        return {
          newTodoItem: '',
          showModal: false  // false로 초기화
        }
      },
      methods: {
        addTodo: function() {
          if (this.newTodoItem !== '') {
            var item = this.newTodoItem.trim();
            this.$emit('addItem', item);
            this.clearInput();
          } else {
            this.showModal = !this.showModal;   // 반대값 넣기
          }
        },
        clearInput: function() {
          this.newTodoItem = '';
        }
      },
      components: {
        Modal: Modal    // 컴포넌트 등록
      }
    }
    </script>
    
    
    
#### vuejs.org에서 긁어온 코드

    <template>
      <transition name="modal">
        <div class="modal-mask">
          <div class="modal-wrapper">
            <div class="modal-container">

              <div class="modal-header">
                <slot name="header">
                  default header
                </slot>
              </div>

              <div class="modal-body">
                <slot name="body">
                  default body
                </slot>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </template>

    <style>
    .modal-mask {
      position: fixed;
      z-index: 9998;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, .5);
      display: table;
      transition: opacity .3s ease;
    }
    .modal-wrapper {
      display: table-cell;
      vertical-align: middle;
    }
    .modal-container {
      width: 300px;
      margin: 0px auto;
      padding: 20px 30px;
      background-color: #fff;
      border-radius: 2px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
      transition: all .3s ease;
      font-family: Helvetica, Arial, sans-serif;
    }
    .modal-header h3 {
      margin-top: 0;
      color: #42b983;
    }
    .modal-body {
      margin: 20px 0;
    }
    .modal-default-button {
      float: right;
    }
    /*
     * The following styles are auto-applied to elements with
     * transition="modal" when their visibility is toggled
     * by Vue.js.
     *
     * You can easily play with the modal transition by editing
     * these styles.
     */
    .modal-enter {
      opacity: 0;
    }
    .modal-leave-active {
      opacity: 0;
    }
    .modal-enter .modal-container,
    .modal-leave-active .modal-container {
      -webkit-transform: scale(1.1);
      transform: scale(1.1);
    }
    </style>
