# API 구현

### install
    
    npm i axios --save


### api제공 url

https://github.com/tastejs/hacker-news-pwas/blob/master/docs/api.md


### 문법

    <template>
        <div>
            <div v-for="user in users">{{ user }}</div>
        </div>
    </template>
    <script>
        import axios from 'axios';
        
        export default {
            data() {
                return {
                    users: []
                }
            },
            created() {
                // 화살표 함수를 사용하지 않을 경우 
                var vm = this;
                axios.get('urls')
                    .then(function(response) {
                        console.log(response);
                        vm.users = response.data;
                    })
                    .catch(function(error) {
                        console.log(error)
                    });
                
                // 화살표 함수를 사용할 경우
                axios.get('urls')
                    .then( response => {
                        console.log(response);
                        this.users = response.data;
                    })
                    .catch(function(error) {
                        console.log(error)
                    });
            }
        }
    </script>





