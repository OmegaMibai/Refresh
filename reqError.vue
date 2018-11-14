<style lang="css" scoped>

.error {
    width: 100%;
    height: 100%;
    background: white;
    font-size: 36px;
    /* px */
    text-align: center;
    position: fixed;
    z-index: 99999;
}

.error img {
    width: 50px;
    height: 50px;
    margin: 50% 0 20px 0;
}

.error p {
    margin: 0 50px;
}

</style>

<template lang="html">
<!-- v-show控制显示隐藏 -->
<div class="error" @click="refresh" v-show="isShow">
    <img src="../assets/ref.jpg">
    <p v-if="promShow">{{prom2}}</p>
    <p v-else>{{prom1}}</p>
</div>

</template>

<script>

export default {
    name: 'reqError',
    //接受父级传过来的名为msg的参数
    props: ['msg'],
    data() {
        return {
            isShow: false,
            promShow: false,
            prom1: '请求失败，请点击空白处刷新！',
            prom2: '请求失败，网络或者服务存在问题，请退出重试！'
        }
    },
    methods: {
        //点击刷新按钮，执行refresh函数
        refresh() {
            if (this.promShow) return;
            this.isShow = false;
            //调用父级名为meth的方法，并把count作为参数传过去
            this.$parent[this.msg.meth](this.msg.count);
        }
    }
}

</script>
