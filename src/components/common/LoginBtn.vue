<!-- 组件说明 -->
<template>
    <div class='btnparent'>
        <div class="loginbtn" @click="registerClick">{{BtnText}}</div>
    </div>
</template>

<script>
    //import x from ''
    export default {
        props:["BtnText"],
        methods:{
            registerClick(){
                this.$emit('TextClick')
            }
        }
    }
</script>

<style lang='less' scoped>
    .btnparent{
        padding: 4.167vw 2.778vw;
        .loginbtn{
            height: 12.5vw;
            background-color: #ff9db5;
            color: #fff;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 6.25vw;
            font-size: 4.444vw;
        }
    }
</style>