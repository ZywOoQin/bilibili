<!-- 组件说明 -->
<template>
    <div class='LoginTop'>
        <div></div>
        <div>{{Text}}</div>
        <div>
            <slot name="right" />
        </div>
    </div>
</template>

<script>
    //import x from ''
    export default {
        props:['Text']
    }
</script>

<style lang='less' scoped>
    .LoginTop{
        height: 12.5vw;
        background-color: #fff;
        display: flex;
        div{
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 4.444vw;
            .fz{
                font-size: 3.611vw;
            }
        }
    }
</style>