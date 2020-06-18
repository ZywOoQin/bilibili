<template>
    <div class='userinfo'>
        <nav-bar></nav-bar>
        <div class="pic">
            <img src="@/assets/bannerTop_new.png" alt="" class="backImg">
        </div>
        <user-detail :userInfo="model"></user-detail>
        <br>
        <user-article></user-article>
    </div>
</template>

<script>
    import NavBar from '@/components/common/NavBar.vue'
    import userDetail from '@/components/userComponent/userDetail.vue'
    import userArticle from '@/components/userComponent/userArticle.vue'
    export default {
        components: {
            NavBar,
            userDetail,
            userArticle
        },
        data () {
            return {
                model:{}
            }
        },
        methods: {
            async userData() {
                const res =  await this.$http.get('/user/' + localStorage.getItem('id'),{
                    headers:{
                        'Authorization':'Bearer ' + localStorage.getItem('token')
                    }
                })
                this.model = res.data[0]
            }
        },
        created() {
            this.userData()
        }
    }
</script>

<style lang='less' scoped>
    .pic{
        height: 33.333vw;
        overflow: hidden;
        .backImg{
            width: 100%;
        }
    }
</style>