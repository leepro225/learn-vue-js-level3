# vue create vue-news 

### 프로젝트 생성
```javascript
vue create vue-news


Vue CLI v.3.2.1
? Please pick a preset:
> default (babel, esling)  ----> enter
Manually select features
```    
    
    
### ESLint

- 문법 오류 잡아주는 플러그인
```javascript
      // 트레일링 콤마 - trailing comma
      components: {
        '컴포넌트 이름': 컴포넌트 내용, // 여기 이거 콤마
      }
```  


### 끄고 싶을 때

- 부분적으로 끄고 싶을 경우
```javascript
// 끄고 싶은 파일.js
<template></template>
<script>
/* eslint-disable */
</script>
```        
        
- 전체 끄고 싶을 경우
```javascript
// vue.config.js 파일 생성(package.json과 동일한 경로)
    module.exports = {
    lintOnSave : false
}
```
        
 참고 : https://cli.vuejs.org/config/#lintonsave
        
