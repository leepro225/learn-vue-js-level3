# slot 을 이용해 데이터 분기처리 하기
```javascript
    // components/UserProfile.vue  -> 컴포넌트
    <template>
        <div class="user-container">
            <div>
                <i class="fas fa-user"></i>
            </div>
            <div class="user-description">
               <slot name="username">
                   <!-- 상위 컴포넌트에서 정의할 영역 -->
               </slot>
            </div>
            <div class="time">
                <slot name="time">
                    <!-- 상위 컴포넌트에서 정의할 영역 -->
                </slot>
            </div>
            <slot name="karma"></slot>
        </div>    
    </template>
    
    
    
    // views/itemView.vue
    <template>
    <div>
        <section>
            <user-profile :info="fetchedItem">
                <div slot="username">{{ fetchedItem.user }}</div>
                <template slot="time">{{ fetchedItem.time_ago }}</template>
            </user-profile>
        </section>
        <section>
            <h2>{{fetchedItem.title}}</h2>
        </section>
        <section>
            <div v-html="fetchedItem.content"></div>
        </section>
    </div>
    </template>

    <script>
    import UserProfile from '../components/UserProfile'
    </script>


    // views/UserView.vue
    <template>
    <div>
        <UserProfile :info="userInfo">
            <div slot="username"> {{ userInfo.id }}</div>
            <template slot="time"> {{ userInfo.created }}</template>
            <div slot="karma"></div>
        </UserProfile>
    </div>
    </template>
    <script>
    import UserProfile from '../components/UserProfile.vue'
    </script>
 ```   

