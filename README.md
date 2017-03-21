## 技术栈
vue2 + vuex + vue-router + webpack + ES6/7 + fetch + sass + flex + svg

##### 注意：由于涉及大量的 ES6/7 等新属性，nodejs 必须是 6.0 以上版本 ，node 7 是先行版，有可能会出问题，建议使用 node 6 稳定版

#### 编译环境
npm run dev
访问 http://localhost:9090

#### 线上版本
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
@click="$router.go(-1)"
this.$router.go(-1);
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
console.log(String.fromCharCode(65))  'A'
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
##### rightPhoneNumber是经过computed属性计算出是否正确的boolen值
``` bash
<span :class="{right_phone_number:rightPhoneNumber}"></span>
```
##### 获取短信验证码 async await的使用
``` bash
async getVerifyCode(){
    if (this.rightPhoneNumber) {
        this.computedTime = 60;
        this.timer = setInterval(() => {
            this.computedTime --;
            if (this.computedTime == 0) {
                clearInterval(this.timer)
            }
        }, 1000)
        //判读用户是否存在
        let exsis = await checkExsis(this.phoneNumber, 'mobile');
        if (exsis.message) {
            this.showAlert = true;
            this.alertText = exsis.message;
            return;
        }else if(!exsis.is_exists) {
            this.showAlert = true;
            this.alertText = '您输入的手机号尚未绑定';
            return;
        }
        //发送短信验证码
        let res = await mobileCode(this.phoneNumber);
        if (res.message) {
            this.showAlert = true;
            this.alertText = res.message;
            return;
        }
        this.validate_token = res.validate_token;
    }
}
```
##### 自定义组件事件
``` bash
父组件
<alert-tip v-if="showAlert" :showHide="showAlert" @closeTip="closeTip" :alertText="alertText"></alert-tip>
methods: {
	closeTip(){
        this.showAlert = false;
    }
}
子组件
<div class="confrim" @click="closeTip">确认</div>
methods: {
    closeTip(){
        this.$emit('closeTip')
    }
}
```