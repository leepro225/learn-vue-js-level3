# 화살표 함수

###  Arrow Function 
    - 함수를 정의할 때 function이라는 키워드를 사용하지 않고 =>로 대체
    - 흔히 사용하는 콜백 함수의 문법을 간결화
    콜백함수 안에서의 스코프는 글로벌(window)를 가리킴
    
    // ES5 함수 정의 방식
    var sum = function(a, b) {
        return a + b;
    };

    // ES6 함수 정의 방식
    var sum = (a. b) => {
        return a + b;
    }
    
    sum(10 ,20);
    
    
### 화살표 함수 사용 예시

    // ES5
    var arr = ["a", "b", "c"];
    arr.forEach(function(value) {
        console.log(value); //a, b, c
    });
    
    // ES6
    const arr = ["a", "b", "c"];
    arr.forEach(value => console.log(value); //a, b, c );
    
    
### 화살표 함수 참고

https://poiemaweb.com/es6-arrow-function
    



