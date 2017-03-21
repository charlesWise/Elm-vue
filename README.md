## 技术栈
vue2 + vuex + vue-router + webpack + ES6/7 + fetch + sass + flex + svg

##### 注意：由于涉及大量的 ES6/7 等新属性，nodejs 必须是 6.0 以上版本 ，node 7 是先行版，有可能会出问题，建议使用 node 6 稳定版

### 编译环境
npm run dev
访问 http://localhost:9090

### 线上版本
npm run build
生成的dist文件夹放在服务器即可正常访问

##### transition使用
``` bash
<transition name="router-fade" mode="out-in">
    <router-view></router-view>
</transition>
.router-fade-enter-active, .router-fade-leave-active {
    transition: opacity .3s;
}
.router-fade-enter, .router-fade-leave-active {
    opacity: 0;
}
```
##### 页面跳转
``` bash
$router.go(-1)
this.$router.push({path:'/delial', query:{id}})  http://localhost:9090/#/delial?id=22
```
##### tag="li" li标签
``` bash
<ul class="citylistul clear">
    <router-link  tag="li" v-for="item in hotcity" :to="'/city/' + item.id" :key="item.id">
        {{item.name}}
    </router-link>
</ul>
<ul>
    <li v-for="(value, key, index) in sortgroupcity" :key="key">
        <h4 class="city_title">{{key}}
            <span v-if="index === 0">（按字母排序）</span>
        </h4>
        <ul>
            <router-link  tag="li" v-for="item in value" :to="'/city/' + item.id" :key="item.id">
                {{item.name}}
            </router-link>
        </ul>
    </li>
</ul>
```
##### String.fromCharCode(i)  根据字符码数获取对应的字符
``` bash
console.log(String.fromCharCode(65))  //'A'
```
##### 获取路由参数
``` bash
this.cityid = this.$route.params.cityid;
```
##### 阻止默认
``` bash
@click.prevent=""   @click.prevent
@click.stop=""   @click.stop
```