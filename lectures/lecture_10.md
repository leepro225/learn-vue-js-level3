# 속성 메서드의 축약 특징 설명

###  Enhanced Object Literals - 향상된 객체 리터럴

 - 객체의 속성을 메서드로 사용할 때 function 예약어를 생략하고 생성 가능

    var dictionary = {
       words : 100,
       // ES5
       // lookup : function() {
         console.log("find words");
       },
       // ES6
       lookup() {
         console.log("find words");
       }
    }
    
    
