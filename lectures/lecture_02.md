# 컴포넌트 생성 및 등록하기 

### 컴포넌트 생성

    <template>
        <div>Something</div>
    </template>
    <script></script>
    <style></style>


### 컴포넌트 등록

    <template>
        <SomethingComponent></SomethingComponet>
    </template>
    <script>
    import SomethingComponent from'./components/SomethingComponent'
    
    export default {
        components : {
            // 컴포넌트 태그명 : 컴포넌트 내용
            'SomethingComponent' : SomethingComponent
        }
    }
    </script>
    <style scoped></style>
    // 이 컴포넌트 안에서만 유효한 스타일 속성, css의 캐스케이딩 원칙을 무시


### input과 v-model

    <template>
      <div>
        <input 
                type="text" 
                v-model="inputText"
                v-on:keyup.enter="addTodo">  // enter를 누르면 저 함수를 실행
        <button v-on:click="addTodo">add</button>
      </div>
    </template>

    <script>
    export default {
        data() {
            return {
                inputText: '',  // input에 입력된 값이 이곳에 바로 바인딩되게 하는 애가 v-model
            };
        },
        methods: {
            addTodo: function() {
                var value = this.inputText;
                this.$emit('add', value);
                // localStorage.setItem(value, value);
                this.clearInput();
            },
            clearInput: function() {
                // 저장 후 input박스 초기화하는 역할
                this.inputText = '';
            },
        },
    };
    </script>
    <style>
    </style>
