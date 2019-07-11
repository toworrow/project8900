<template>
<div class='login-container'>
 <el-card class="login-box">
  <img src="../../assets/images/logo_index.png">
 <el-form ref="loginForm"  :status-icon="true"  :model="loginForm" :rules="loginRules">

        <el-form-item prop="moblie">
          <el-input type="text" placeholder="请输入手机号"  v-model="loginForm.moblie" ></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-input placeholder="请输入验证码" v-model="loginForm.code" style="width:200px" ></el-input>
          <el-button style="float:right">发送验证码</el-button>
        </el-form-item>
        <el-form-item>
          <el-checkbox :value="true"></el-checkbox>

          我已阅读并同意 <el-link type="primary">用户协议</el-link> 和 <el-link type="primary">隐私条款</el-link>
          </el-form-item>
          <el-form-item>
          <el-button style="width:100%" type="primary" @click="login()">登 录</el-button>
         </el-form-item>
      </el-form>
  </el-card>
</div>
</template>
<script>
export default {
  methods: {
    login () {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          // 提出请求
          this.$http
            .post('http://ttapi.research.itcast.cn/mp/v1_0/authorizations',
              this.loginForm)
            .then(res => {
              this.$router.push('/')
            })
            .catch(() => {
              this.$message.error('手机号或验证码有误')
            })
        }
      })
    }
  },
  data () {
    const checkMobile = (rule, value, callback) => {
      if (/^1[3-9]\d{9}$/.test(value)) {
        callback()
      } else {
        callback(new Error('手机格式不正确'))
      }
    }
    return {
      loginForm: {
        moblie: '',
        code: ''
      },
      loginRules: {
        moblie: [
          { required: true, message: '请输入手机号', trigger: 'blur' },
          { validator: checkMobile, trigger: 'blur' }

        ],
        code: [
          { required: true, message: '请输入验证码', trigger: 'blur' },
          { len: 6, message: '请输入6位数字', trigger: 'blur' }
        ]
      }
    }
  }

}
</script>
<style scope lang="less">
.login-container{
    width:100%;
    height:100%;
    position:absolute;
    left:0;
    top:0;
    background:url('../../assets/images/login_bg.jpg') no-repeat center / cover;
}
.login-box{
     width: 400px;
    height: 320px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
}
img{
     display: block;
      width: 200px;
      margin: 5px auto;
}
</style>
