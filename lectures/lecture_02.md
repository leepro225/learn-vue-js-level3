# cli

### vue init webpack-simple

클론한 폴더 vue-news에서 시작
```
vue init webpack-simple vue-news


? Project name vue-news   ---> enter
? Project description A Vue.js project   ---> enter
? Author leepro225 <leepro225@gmail.com>   ---> enter
? License MIT   ---> enter
? Use sass? (y/n)   ---> N
```    


### vue create

```
vue create vue-cli3

// 설치가 안될거임 이런 문구 뜨면서

vue create is a Vue CLI 3 only command................................
// 명령어를 쓰려면 업데이트 해야한다는 뜻


npm install -g @vue/cli

Vue CLI v3.2.1
? Please pick a preset:
> Default (babel, eslint)    ---> enter
Maunally select features
``` 
 
 ### Vue CLI2.x vs CLI3.x 버전 비교
 
 - 명령어 
    - 2.x : vue init '프로젝트 템플릿 이름' '파일 위치'
    - 3.x : vue create '프로젝트 이름'
    
 - 웹팩 설정 파일
    - 2.x : 노출 O
    - 3.x : 노출 X
    
 - 프로젝트 구성
    - 2.x : 깃헙의 템플릿 다운로드
    - 3.x : 플러그인 기반으로 기능 추가
    
 - ES6 이해도
    - 2.x : 필요 x
    - 3.x : 필요 O



