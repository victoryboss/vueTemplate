<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <p>
            For guide and recipes on how to configure / customize this project,<br>
            check out the
            <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
        </p>
        <h3>Installed CLI Plugins</h3>
        <ul>
            <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank"
                   rel="noopener">babel</a></li>
            <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank"
                   rel="noopener">eslint</a></li>
        </ul>
        <h3>Essential Links</h3>
        <ul>
            <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
            <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
            <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
            <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
            <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
        </ul>
        <h3>Ecosystem</h3>
        <ul>
            <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
            <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
            <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank"
                   rel="noopener">vue-devtools</a></li>
            <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
            <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
        </ul>
        <span>ElementUI示例 </span>
        <el-switch
                v-model="value2"
                active-color="#13ce66"
                inactive-color="#ff4949">
        </el-switch>
        <input v-validate="'required|email'" name="email" type="text">
        <span>{{ errors.first('email') }}</span>
        <div>
            <h1 @click="addCount">list{{count}}</h1>
            <ul>
                <li v-for="item in list"  :key="item.id">
                    {{item.title}}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import {mapState, mapGetters, mapActions} from 'vuex'
    import store from '../store'

    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                value1: true,
                value2: true
            }
        },
        computed:{
            ...mapState({
                list: state => state.hello.list,
                count: state => state.hello.count,
            }),
            ...mapGetters('hello', {
                hasMore: 'hasMore'
            })
        },
        mounted() {
            store.dispatch('hello/changeCount', 1)
            this.fetchList()
            if (!this.loadjs.isDefined('videoBox')) {
                this.loadjs('//newbuz.360buyimg.com/video/4.6/videoBox.js', 'videoBox', {
                    success: function() { /* foo.js & bar.js loaded */ console.log(1)},
                    error: function() { /* at least one path didn't load */ },
                    numRetries: 3
                });
            }
            // this.axios.get('/news/index').then(function (res) {
            //     console.log(res);
            // });
        },
        methods:{
            ...mapActions('hello', {
                fetchList: 'fetchList',
                changeCount:'changeCount'
            }),
            addCount(){
                this.changeCount(10);
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
