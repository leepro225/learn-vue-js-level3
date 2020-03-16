# Mixins

믹스인(Mixins)은 여러 컴포넌트 간에 공통으로 사용하고 있는 로직, 기능들을 재사용 하는 방법. 믹스인에 정의할 수 있는 재사용 로직은 data, methods, created 등과 같은 컴포넌트 옵션.


### 믹스인 코드 형식
```javascript
const HelloMixins = {
  // 컴포넌트 옵션 (data, methods, created 등);
}

new Vue({
  mixins: [HelloMixins] // 배열로 믹스인들을 추가
})
```


### 믹스인 예시

```javascript
<script>
// src/mixins/mixins.js
export const DialogMixin = {
  data() {
    return {
      dialog: false
    }
  },
  methods: {
    showDialog() {
      this.dialog = ture;
    },
    closeDialog() {
      this.dialog = false;
    }
  }
}

</script>
<script>
import { DialogMixin } from '../src/mixins/mixins.js'

export default {
  mixins: [DialogMixin], // 믹스인을 주입
  methods: {
    submitForm() {
      axios.post('login', {
        id : this.id,
        pw : this.pw
      })
      .then(() => this.closeDialog()) //꺼내서 사용
      .catch((error) => new Error(error));
    }
  }
}

</script>
