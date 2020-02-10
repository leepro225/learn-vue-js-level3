# Modules

###  자바스크립트 모듈화 방법

 - 자바스크립트 모듈 로더 라이브러리(AMD, Commons JS) 기능을 js 언어 자체에서 지원  
 - 호출되기 전까지는 코드 실행과 동작을 하지 않는 특징이 있음  
 
    // libs/math.js
    export function sum(x, y) {
        return x + y;
    }
    export var pi = 3.141593;
    
    // main.js
    import {sum} from 'libs/math.js';
    sum(1, 2);
    
 - ES5에서와 달리 ES6에서는 파일 단위로 스코프가 나뉨  
 
 
 

### default export

    // util.js
    export default function(x) {
        return console.log(x);
    }
    
    // main.js
    import util from `util.js`;
    console.log(util); // function(x) {return console.log(x);}
    util("hi");

    // app.js
    import log from `util.js`;  // 다른 이름으로도 가져와서 사용 가능
    console.log(log); // function(x) {return console.log(x);}
    log("hi");
    
- default 는 하나의 파일에 하나만 쓸 수 있다. 인캡슐리션. 모듈화 한다...?
