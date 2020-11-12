<template>

  <body id="poster">
    <el-form class="login-container" label-position="left" label-width="0px">
      <el-alert v-if="this.showWrong" title="登录名或密码错误" type="error" center show-icon>
      </el-alert>
      <h3 class="login_title">欢迎</h3>
      <h3 class="login_title"></h3>

    </el-form>
  </body>
</template>

<script>

export default {
  name: 'Login',
  data () {
    return {
      loginForm: {
        username: 'admin',
        password: '123'
      },
      responseResult: [],
      showWrong: false //显示错误登录代码
    }
  },
  methods: {
    login () {
      this.showWrong = false,
        this.$axios
          .post('/login', {
            username: this.loginForm.username,
            password: this.loginForm.password
          })
          .then(successResponse => {
            if (successResponse.data.code === 200) {
              this.$router.replace({ path: '/index' })
            }
            else {
              this.showWrong = true
            }
          })
          .catch(failResponse => {
          })
    }
  }
}
</script>
<style scoped>
#poster {
  background: url("../assets/ezm.jpg") no-repeat;
  background-position: center;
  height: 100%;
  width: 100%;
  background-size: cover;
  position: fixed;
}
body {
  margin: 0px;
}
.login-container {
  border-radius: 15px;
  background-clip: padding-box;
  margin: 90px auto;
  width: 350px;
  padding: 35px 35px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}
.login_title {
  margin: 0px auto 40px auto;
  text-align: center;
  color: #505458;
}
</style>
