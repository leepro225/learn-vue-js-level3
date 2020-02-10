# const and let 새로운 변수 선언 방식

### const & let

 - 블록단위의 변수선언 방식
 - const : 한번 선언한 값에 대해서 변경할 수 없음(상수 개념)
 - let : 한번 선언한 값에 대해서 다시 선언할 수 없음


### ES5의 특징 - 변수의 scope
 
 - 기존 자바스크립트(ES5)는 {} 에 상관없이 스코프가 설정됨
 
        var sum = 0;
        for (var i =1; i <= 5; i++) {
           sum = sum + i;
        }
        console.log(sum);
        console.log(i);
  
  
  
### ES5의 특징 - Hoisting

  - Hoisting 이란 선언한 함수와 변수를 해석기가 가장 상단에 있는 것처럼 인식한다.
  - js 해석기는 코드의 라인 순서와 관계 없이 함수선언식과 변수를 위한 메모리 공간을 먼저 확보한다.
  (함수 표현식은 해당이 안됨)
  - 따라서, function a() (함수선언문)와 var(변수)는 코드의 최상단으로 끌어 올려진 것(hoisted)처럼 보인다.

        function() willBeOveridden() {
          return 10;
        }
        willBeOveridden(); // 5
        function() willBeOveridden() {
          return 5;
        }
  
  
  
### 아래와 같은 코드를 실행할 때 자바스크립트 해석기가 어떻게 코드 순서를 재조정할까?

    var sum = 5;
    sum = sum + i;
    
    function sumAllNumber() {
     // ...
    }
    
    var i = 10;
    
일단은 var와 function을 다 끌어 올리고 대입과 할당은 나중에 한다!!!!

    // #1 - 함수 선억식과 변수 선언을 hoisting
    var sum;
    function sumAllNumbers() {
     // ...
    }
    var i;
    
    // #2 - 변수 대입 및 할당
    sum = 5;
    sum = sum + i;
    i = 10;
    
    
 ### ES6 - {}블록 단위로 변수의 범위가 제한됨
 
     let sum = 0;
     for (let i = 1; i <= 5; i++) {
       sum = sum + i;
     }
     console.log(sum); // 10
     console.log(i);  // Uncaught ReferenceError: i is not defined
     
 
    
### ES6 - const로 지정한 값 변경 불가능

    const a = 10;
    a = 20; // Uncaught TypeError: Assignment to constant variable
    
하지만, 객체나 배열의 내부는 변결할 수 있다.

    const a = {};
    a.num = 10;
    console.log(a); // {num : 10}
    
    const a = [];
    a.push(20);
    console.log(a); // 20


