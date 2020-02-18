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


# API 폴더 구조

### 반복되는 코드를 줄이기 위해 구조화

        // src/api/index.js 폴더와 파일 생성
        import axios from 'axios';
        
        // 1.HTTP Request & Response와 관련된 기본 설정
        const config = {
            baseUrl : 'https://api.hnpwa.com/v0'
        }
        
        // 2.API 함수들을 정리
        function fetchNewsList() {
            return axios.get(`${config.baseUrl}news/1.json`);
        }
        
        export {
            fetchNewsList
        }


        // src/views/NewsView.vue
        import { fetchNewsList } from '../api/index.js'
        export default {
            created() {
                fetchNewsList()
                    .then(res => {
                        console.log(res);
                    })
                    .catch(err => {
                        console.log(err);
                    });
            }
        }
