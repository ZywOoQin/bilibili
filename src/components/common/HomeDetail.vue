<template>
    <div v-if="detailitem" @click="pathPush">
        <div class="detailItem">
            <div class="imgparent">
                <img :src="detailitem.img">
                <div class="bottom">
                    <div class="icon-play2"><span class="video">1233</span></div>
                    <div class="icon-file-text"> <span class="comment">{{!detailitem.commentlen ? 66 : detailitem.commentlen}}</span> </div>
                </div>
            </div>
            <p>{{detailitem.name}}</p>
        </div>
    </div>
</template>

<script>
    //import x from ''
    export default {
        props:['detailitem'],
        data () {
            return {

            }
        },
        methods: {
            pathPush() {
                if(this.$route.path != `/article/${this.detailitem.id}`) {
                    this.$router.push(`/article/${this.detailitem.id}`)
                }
            }
        }
    }
</script>

<style lang='less' scoped>
    .detailItem{
        p{
            font-size: 3.333vw;
            padding: 0.833vw 0;
        }
        .imgparent{
            position: relative;
            img{
                width:100%;
                height:27.778vw;
            }
            .bottom{
                padding: 1.389vw 1.944vw;
                position: absolute;
                bottom: 0.556vw;
                background: linear-gradient(0deg,rgba(0,0,0,.85),transparent);
                justify-content: space-between;
                color: white;
                display: flex;
                left: 0;
                right: 0;
            }
        }
    }
</style>