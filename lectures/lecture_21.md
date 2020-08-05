# 라이브러리 모듈화

### 123
 - 함수의 앞에 async를 붙여주고 내부 로직 중 비동기 처리하고 싶은 함수 앞에 await를 붙인다. 이때 await가 붙은 함수는 Promise 객체를 반환한다.
 
       async FETCH_NEWS(context) {
        try {
            const response = await fetchNewsList();
            context.commit('SET_NEWS', response.data);
            return response;
        } catch (error) {
            console.log(error);
        }
        
       }
       
       function fetchNewsList() {
       return axios.get(`${config.baseUrl}news/1.json`);
       }

or

    async FETCH_JOBS({ commit }) {
        const response = await fetchJobsList()
        commit('SET_JOBS', response.data);
        return response;
    }

    function fetchJobsList() {
        try {
            return axios.get(`${config.baseUrl}jobs/1.json`);
        } catch(error) {
            console.log(error);
        }
    }
