# plugins

### plugins 사용 이유
 - 라이브러리를 컴포넌트 마다 불러오는 필요한 코드들이 생기게 됨. 그래서 plugins폴더로 모듈화
 
       // like this
       import Chart from 'chart.js';
 
     
       // so, 아래 경로에 plugins 폴더와 파일 생성    
       └assets
       └components
       └plugins
         └ChartPlugin.js

     
     
       // 뷰에서 제공하는 플러그인은 Vue.use() 사용함.
       // $_ -> vue에서 사용하는 다른 변수들과 중복되지 않게 하기 위해 vue에서 공식적으로 권장
       // ChartPlugin.js
       import Chart from 'chart.js';
     
       export default {
         install(Vue) {
           Vue.prototype.$_Chart = Chart;
         }
       }
     

       // main.js
       import ChartPlugin from './plugins/ChartPlugin.js';
      
       Vue.use(ChartPlugin);
     
     
       // 이러케 하면 전역에서 this.$_Chart 로 접근 가능
