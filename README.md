## 技术栈
vue2 + vuex + vue-router + webpack + ES6/7 + fetch + sass + flex + svg

#### 注意：由于涉及大量的 ES6/7 等新属性，nodejs 必须是 6.0 以上版本 ，node 7 是先行版，有可能会出问题，建议使用 node 6 稳定版

### 编译环境
npm run dev
访问 http://localhost:9090

### 线上版本
npm run build
生成的dist文件夹放在服务器即可正常访问

### transition使用
<transition name="router-fade" mode="out-in">
    <router-view></router-view>
</transition>

.router-fade-enter-active, .router-fade-leave-active {
    transition: opacity .3s;
}
.router-fade-enter, .router-fade-leave-active {
    opacity: 0;
}

###返回上一个
$router.go(-1)