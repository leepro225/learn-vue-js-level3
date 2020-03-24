    ```javascript
    <template>
        <div>
            <ul class="news-list">
            <li v-for="item in listItems" v-bind:key="item.id" class="post">
                <div class="points">
                    {{item.points || 0}}
                </div>
                <div>
                    <p class="news-title">
                        <template v-if="item.domain">
                            <a v-bind:href="item.url">
                                {{ item.title }}
                            </a>
                        </template>
                        <template v-else>
                            <router-link v-bind:to="`item/${item.id}`">
                                {{ item.title }}
                            </router-link>    
                        </template>

                    </p>
                    <small>
                        {{item.time_ago}}
                        by
                        <router-link v-if="item.user"                     
                                     v-bind:to="`/user/${item.user}`"
                                     class="link-text"></router-link>
                        <a v-else :href="item.url">{{item.domain}}</a>
                    </small>
                </div>
            </li>
        </ul>
        </div>    
    </template>
    <script>
    export default {
        created() {
            const name = this.$route.name;
            let actionsName = '';
            if (name === 'news') {
               actionsName = 'FETCH_NEWS';
            } else if (name === 'ask') {
               actionsName = 'FETCH_ASK';
            } else if (name === 'jobs') {
               actionsName = 'FETCH_JOBS';
            }
            this.$store.dispatch(actionsName);
        },
        computed: {
            listItems() {
                const name = this.$route.name;
                if (name === 'news') {
                    return this.$store.state.news;
                } else if (name === 'ask') {
                    return this.$store.state.ask;
                } else if (name === 'jobs') {
                    return this.$store.state.jobs;
                }    
                return 0     
            }
        }
    }
    </script>
```
