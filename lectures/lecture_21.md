# refs, DOM에 접근하는 방법

### refs
 - 접근하고자 하는 태그에 ref를 적어주면 refs배열에 값이 추가된다. 접근할때는 $refs.하위태그에 입력한 ref
 
       <template>
        <div>
          <canvas ref="barChart"></canvas>
        </div>
       </template>
       <script>
        export default {
          mounted() {
            var barChart = this.$refs.barChart;
          }
        }
       </script>


