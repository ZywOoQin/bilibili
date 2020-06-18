<template>
  <div>
      <login-top Text="注册bilibili">
          <div slot="right" class="fz" @click="$router.push('/login')">用户登录</div>
      </login-top>
        <login-text label="姓名" 
            style="margin:15.001px 0;" 
            placeholder="请输入姓名"
            @contentWatch="res => model.name = res"
            >
        </login-text>

        <login-text label="账号" 
        placeholder="请输入账号"
         @contentWatch="res => model.username = res"
         >
        </login-text>

        <login-text label="密码" 
            placeholder="请输入密码" 
            type="password"
            @contentWatch="res => model.password = res"
        >
        </login-text>

        <login-btn BtnText="注册" @TextClick="AjaxInsert"></login-btn>
  </div>
</template>

<script>
import LoginTop from '@/components/common/LoginTop.vue'
import LoginText from '@/components/common/LoginText.vue'
import LoginBtn from '@/components/common/LoginBtn.vue'
export default {
    data() {
        return {
            model:{}
        }
    },
    components:{
        LoginTop,
        LoginText,
        LoginBtn
    },
    methods:{
        async AjaxInsert() {
            let rulgn = /^.{1,16}$/
            let rulg = /^.{6,16}$/
            if(rulgn.test(this.model.name) && rulg.test(this.model.username)&& rulg.test(this.model.password)){
                const res =  await this.$http.post('/register',this.model)
                this.$msg.fail(res.data.msg)
                localStorage.setItem('token',res.data.objtoken) 
                localStorage.setItem('id',res.data.id) 
                setTimeout(() => {
                    this.$router.push('/userinfo')
                },1000)
            }else{
                this.$msg.fail('格式不正确,请重新输入!')
            }
        }
    }
}
</script>

<style lang="less" scoped>
  
</style>