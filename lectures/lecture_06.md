# this

### 첫번째 this
```javascript
    // 전역에서 this는 window를 가리킨다.
    // console에서
    
    > this
    < Window {postMesssage: f, blur : f,,,}
```    
    
### 두번째 this

```javascript
    // 함수 내에서 this는 window를 가리킨다.
    // console에서
    
    function sum(a, b) {
        console.log(this);
        return a + b;
    }
    sum(10 + 5);
    > Window {postMesssage: f, blur : f,,,}
```    
   
###  세번째 this

```javascript
    // 생성자 함수 내에서의 this는 인스턴스 자체를 가리킨다.
    // console에서
    
    function Vue(el) {
        console.log(this);
        this.el = el;
    }
    new Vue('#app');
    > Vue {}
```

### 네번째 this

```javascript
    // 비동기 호출, 콜백함수 안에서의 this는 undefined
    // 따라서 화살표 함수를 사용해 줘야 한다.
    fetchNewsList()
        .then(res => {
            this.users = res.data;
        })
        .catch(err => {
            console.log(err);
        });
```
