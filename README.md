# study_vue
## ES6的常用语法
    -- 变量的定义
        -- var
        -- let
        -- const
    -- 模板字符串
        -- ``
        -- ${}
    -- 箭头函数
        -- 注意this跟普通函数的区别
    -- 类
        -- class
        -- extends
        -- constructor
        -- 子类没有this 需要用super()
    -- 数据的解构
        -- 注意语法
## Vue的常用指令
    -- v-text
    -- v-html
    -- v-if
    -- v-show
    -- v-for
    -- v-bind
    -- v-on
    -- v-model
        -- input
        -- select
        -- textarea
    -- 指令的修饰符
        -- .lazy
        -- .number
        -- .trim
    -- 自定义的指令
        -- Vue.directive("指令名称", function(el, binding){
                el 绑定指令的标签元素
                binding 指令的所有信息
        })
    -- 计算属性
        -- 放入内存
        -- 当数据改变的时候才会重新计算
    -- 获取DOM
        -- 给标签增加属性 ref = "xxxx"
        -- this.$refs.xxxx

## Vue的组件
    -- 全局注册
        -- Vue.component("组件的名称", {
            template: ``,
            data(){
                return {
                    xxx:xx
                }
            }
        })
    -- 局部注册
        -- let my_com = {
            template: ``,
            data(){
                return {
                    xxx:xx
                }
            }
        }
        -- 在APP里components： {
            my_com: my_com
        }
        -- <my_com></my_com>
    -- 子组件的组件
        -- 在父组件里components: {
            child: child
        }
        -- 在父组件的template里面<child></child>
    -- 通信
        -- 父子通信
            -- 在父组件里给子组件绑定属性
                --<child :xxx="值"></child>
            -- 子组件通过props接收
        -- 子父通信
            -- 子组件提交事件
                -- this.$emit("事件名称"，要传的数据)
            -- 在父组件给子组件绑定事件
                --<child @xxx="自己处理的方法"></child>
        -- 非父子通信
            -- 定义中间调度器
                -- let Event = new Vue()
            -- 其中一个组件要向中间调度器提交事件
                -- Event.$emit("事件名称"，要传的数据)
            -- 另一个组件要监听调度器中的事件
                -- mounted(){
                    Event.$on("事件名称", function(data){
                            do something.....
                    })
                }
    -- 混合
        -- mixins 用于代码复用
    -- 插槽
        -- 为组件做内容分发的接口
        -- 命名插槽
## Vue的路由
    -- 路由的注册
        -- let url = [
            {
                path: "/",
                component: {
                    template: ``
                }
            }
        ]
        -- let router = new VueRouter({
            routes: url
        })
        -- 在APP中注册注册路由
            -- new Vue({
                el: "#app",
                router: router
            })
        -- <router-link :to="{name: 'xx'}">首页</router-link>
        -- <router-view></router-view>
    -- 子路由的注册
        -- children: [
                {
                    path: "xxx",
                    component: {
                        template: ``
                    }
                }
            ]
    -- 路由的参数
        -- path: "/user/:name"
        -- this.$route
            -- 路由的所有信息
            -- fullpath
            -- path
            -- params
            -- query
            -- meta
        -- this.$router
            -- VueRouter 实例对象
    -- 路由的命名
        -- 注意to参数要动态绑定
    -- 手动更新路由
        -- this.$router.push("///")
    -- 路由的钩子函数
        -- router.beforeEach(function(to, from, next){
                to 你要去哪
                form 你从哪来
                next 接下来做什么
                    -- false 中断路由
                    -- 空  正常执行
                    -- 路径  调转到该路径
        })
        -- router.afterEach(function(to, from){
                to 你要去哪
                form 你从哪来
        })
    -- 命名的路由视图
        -- 一个路由对应多个组件的时候
        -- <router-view name="组件的名称"></router-view>
## 生命周期
    -- beforeCreate
    -- created
    -- beforeMount
    -- mounted
    -- beforeUpdate
    -- updated
    -- beforeDestroy
    -- destroyed
    -- 数据监听
        -- watch: {
            数据：{
                handler: function(val, oldVal){

                },
                deep: true
            }
        }
        -- 数据
            -- app.$set(数据, index/key, value)
## npm webpack vue-cli
    -- npm
        -- npm 是node.js 包管理工具
        -- npm init -y
            -- package.json
        -- npm install xxxx@0.0.0 下载包
        -- npm uninstall xxx 卸载
        -- npm update xxx 更新
        -- npm list -g
    -- webpack  打包工具 4以上版本
        -- webpack不独立存在了需要有webpack-cli
        -- npm i webpack webpack-cli
        -- 默认的打包入口文件 需要手动创建src
            -- src/index.js
        -- 出口文件在dist目录下的main.js
        -- webpack --mode development/production
    -- vue-cli 3
        -- npm i -g @vue/cli
        -- vue create xxx
        -- cd /xxx   npm run serve
        -- 目录结构
            -- src 工作目录
                -- components
                -- assets
                    -- 静态资源
                -- APP.vue
                -- main.js
            -- public
                -- index.html
            -- node_moudeles
            -- package.json
## Vuex
    -- 集中式状态管理架构
    -- 配置
        -- npm install vuex
        -- import vuex from "vuex"
        -- Vue.use(vuex)
        -- let store = new vuex.Store({
                state: {
                    xxx: xxx
                },
                getters: {
                    xxx: function(state, getters){
                        return 处理后的数据
                    }
                },
                mutations: {}
        })
        -- const app = new Vue({
            el: "#app",
            store: store
        })
    -- 获取vuex中的数据
        -- this.$store.state.xxx
        -- this.$store.getters.xxx
    -- 更改vuex中的数据
        -- this.$store.commit("事件名称",data)
        -- mutations: {
            "事件名称": function(state, data){
                    state.xxx = data
            }
        }
## Axios
    -- 配置
        -- npm install axios
        -- import axios from "axios"
        -- Vue.prototype.$axios = axios
    -- this.$axios.request({
        url: "api....",
        method: "get",
        data: {},
        params: {}
    }).then(function(data){
        注意this
    }).catch(function(data){

    })
    -- 跨域问题
## restful
    -- REST 表征性状态转移 （资源状态转移）
        -- 资源
        -- URI 统一资源标志符
           URL 统一资源定位符
        -- 统一资源接口
            -- 对资源只开放一个接口
            -- 根据HTTP请求方式的不同对资源进行不同的操作
            -- 一定要遵循HTTP请求方式的语义
        -- 前后端传递的是资源的表述 并不是资源的本身
            -- Accept
                -- 我能够解析的数据类型
            -- ContentType
                -- 给你响应的数据类型
        -- 资源的状态
        -- 通过超链接的指引来告诉用户还有哪些资源状态可以进入
    -- restful
        -- 只要遵循这个REST风格 我们就叫做restful架构
    -- 规范 10条
        -- 核心思想
            -- 面向资源去编程 url尽量用名词 不要用动词
            -- 根据method不同对资源进行不同操作
        -- 在url中体现
            -- 版本
            -- api
            -- 过滤条件
            -- https
        -- 返回的要求
            -- 携带状态码
            -- 返回值
                -- get 返回查看所有数据
                -- post 返回新增的数据
                -- put/patch 返回更新这条数据
                -- delete 返回值为空
            -- 返回携带错误信息
            -- 携带超链接

[vue-cli3](https://blog.csdn.net/qq_36407748/article/details/80739787 "Markdown")

[虚拟环境](https://blog.csdn.net/weixin_39036700/article/details/80711565?utm_source=blogxgwz0 "Markdown")
