<template>
    <div class="editViews">
        <nav-bar class="mb"></nav-bar>
        <div class="uploadfile">
            <div class="uploadimg"><van-uploader preview-size="100vw" :after-read="afterRead" /></div>
            <edit-banner left="头像">
                <img :src="model.user_img"  slot="right" alt="" v-if="model.user_img">
                <img src="@/assets/default_img.jpg"  slot="right" alt="" v-else>
            </edit-banner>
        </div>
        <edit-banner left="昵称" @bannerClick="show = true">
          <a href="javascript:;" slot="right">{{model.name}}</a>
        </edit-banner>
        <edit-banner left="账号">
            <a href="javascript:;" slot="right">{{model.username}}</a>
        </edit-banner>
        <edit-banner left="性别" @bannerClick="gendershow = true">
            <a href="javascript:;" slot="right">{{model.gender ? '男' : '女'}}</a>
        </edit-banner>
        <edit-banner left="个性签名" @bannerClick="textshow = true">
          <a href="javascript:;" slot="right">{{model.user_desc}}</a>
        </edit-banner>

        <div class="editback" @click="$router.back()">返回个人中心</div>

        <van-dialog v-model="show" 
        title="昵称" 
        show-cancel-button 
        @confirm="confirmClick"
        @cancel="content = ''"
        >
            <van-field v-model="content" autofocus  class="marb"/>
        </van-dialog>


        <van-dialog 
        v-model="textshow"
        title="个性签名"
        show-cancel-button
        @confirm="textareaClick"
        @cancel="content = ''"
        >
            <van-field v-model="content" type="textarea" autofocus />
        </van-dialog>

        <van-action-sheet v-model="gendershow" cancel-text="取消" :actions="actions" @select="onSelect" />
    </div>
</template>

<script>
    import NavBar from '@/components/common/NavBar.vue'
    import editBanner from '@/components/common/editBanner.vue'
    export default {
        components: {
            NavBar,
            editBanner
        },
        data () {
            return {
                model:{},
                show:false,
                textshow:false,
                gendershow:false,
                content:'',
                actions: [
                    { name: '男',val:1 },
                    { name: '女',val:0 },
                ],
            }
        },
        methods: {
            //进入组件调取数据渲染页面
            async selectUser() {
                const res =  await this.$http.get('/user/' + localStorage.getItem('id'))
                this.model = res.data[0] 
            },
            async afterRead(file) {
                const fromdata = new FormData()
                fromdata.append('file',file.file)
                const res =  await this.$http.post('/upload',fromdata)
                this.model.user_img = res.data.url
                this.UserUpdate()
            },
            async UserUpdate() {
                const res = await this.$http.post('/update/' + localStorage.getItem('id'),this.model)
                if(res.data.code == 200){
                    this.$msg.success('修改成功')
                } 
            },
            confirmClick() {
                let rulg = /^.{1,16}$/
                if(rulg.test(this.content)){
                    this.model.name =  this.content
                    this.UserUpdate()
                    this.content = ''
                }else{
                    if(this.content.length === 0){
                        this.$msg.fail('昵称不能为空，请重新修改')
                    }else{
                        this.$msg.fail('昵称不能超过16位，请重新修改')
                        this.content = ''
                    }
                }
            },
            textareaClick() {
                let rulg = /^.{0,16}$/
                if(rulg.test(this.content)){
                    this.model.user_desc = this.content
                    this.UserUpdate()
                    this.content = ''
                }else{
                    this.$msg.fail('个性签名不能超过16位，请重新修改')
                    this.content = ''
                }
            },
            onSelect(data) {
                this.model.gender = data.val
                this.UserUpdate()
                this.gendershow = false
            }
        },
        created(){
            this.selectUser()
        }
    }
</script>

<style lang='less' scoped>
    .editViews {
        .mb{
            margin-bottom:2.778vw;
        }
        .uploadfile{
            overflow: hidden;
            position: relative;
            .uploadimg{
                opacity: 0;
                position: absolute;
            }
        }
        img{
            height: 12.778vw;
            width: 12.778vw;
            border-radius: 50%;
        }
        a{
            color: #333;
        }
        .marb{
            margin-bottom: 1.389vw;
        }
        .editback{
            margin-top: 5.556vw;
            background-color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            color: #999;
            padding: 4.167vw 0;
            font-size: 4vw;
        }
    }
</style>