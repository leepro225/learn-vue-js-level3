# Callback과 Promise

### Callback
- 어떤 함수가 종료되자마자 어떤 함수가 실행되게 하는 것  
- 자바스크립트는 인자로 함수를 넘길 수 있기 때문에 가능. 그 함수가 callback함수  

```javascript
      <script>
      funcion fetchData() {
        // 순서 1번
         const result = [];
         
        // 순서 2번
        $.ajax({
         url : 'https://something.com/news'
         success : function(data) {
          console.log('데이터 호출 결과', data);
          result = data;
          // console.log('함수 결과', result); 결괏값을 받고 난 후 result를 보려면 여기서 찍어야함 이게 콜백함수. 이게 많아지면 깊어짐
         } 
        });
        
        // 순서 3번
        console.log('함수 결과', result);
      }
      </script>
```      
 - 순서대로 실행될 것 같지만 3번 보다 2번이 먼저 찍힘, 그래서 console.log()를 success안으로 옮김.이게 콜백함수  
 - 참고 : https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/  
 
 
 
 ### Promise
 - 성공하면 다음 함수 실행해--> ajax에서 success 제공  
 - Promise가 등장
 
```javascript
       <script>
       function callAjax() {
         return new Promise(function(resolve, reject) {
           $.ajax({
             url : 'https://something.com/news';
             success : function(data) {
               resolve(data); // 성공하고나서 이 프로미스를 마칠때 resolve()
             }
           });
         });
       }
       funcion fetchData() {
        // 순서 1번
         const result = [];
         
         callAjax()  // -> 프라미스에서 resolve되고나면 결괏값 data받아서 then실행, 더 직관적
          .then(function(data) {
             console.log('데이터 호출 결과', data);
             result = data;
             console.log('함수 결과', result); 
          }).
          catch();
          
        // 순서 3번
        // console.log('함수 결과', result);
       }
       </script>
 ```     
      
      
 - 참고
 프로미스 쉽게 이해하기 글 주소 : https://joshua1988.github.io/web-development/javascript/promise-for-beginners/  
 Promise MDN 주소 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise  
 
 
 
