<template>
  <div class="loginPage">
    <div class="img">
      <img src="../assets/MovieHub.png" height="119" width="405"/>
    </div>
    <div class="box">
      <h2>LOGIN</h2><br>
      <input type="text" v-model="username" placeholder="用户名"><br>
      <input type="password" v-model="password" placeholder="密码"><br>
    </div>
    <div class="button">
      <button v-on:click="userLogin">登陆</button>
      <button v-on:click="userRegister">注册</button>
      <button v-on:click="findBackPassword">忘记密码</button>
    </div>
    <common-footer></common-footer>
  </div>
</template>

<script>
import CommonFooter from "../components/CommonFooter";
export default {
  name: "loginPage",
  components:{
    CommonFooter
  },
  data(){
    return {
      username: '',
      password: '',
    }
  },
  methods: {
    //用户登陆
    userLogin:function (event) {
      this.$http.post('http://localhost:3000/users/login',{
        username: this.username,
        password: this.password
      }).then((data) => {
        if (data.body.status ===1) {
          alert(data.body.message)
        }
        else {
          alert(data.body.message)
          localStorage.setItem('token',data.body.data.token)
          localStorage.setItem('username',data.body.data.user[0].username)
          localStorage.setItem('_id',data.body.data.user[0]._id)
          this.$router.go(-1)
        }
      })
    },
    //注册跳转页面
    userRegister: function (event) {
      this.$router.push({path: 'register'})
    },
    //注册跳转页面
    findBackPassword: function (event) {
      this.$router.push({path: 'findPassword'})
    }
  }
}
</script>

<style scoped>
.loginPage{
  width: 50%;
  height: 50%;
  margin: 10% auto;
}
.img{
  text-align: center;
}
.box{
  text-align: center;
}
.box input{
  margin-top: 10px;
  border-radius: 10px;
  width: 200px;
  height: 30px;
}
.button{
  margin-top: 30px;
  margin-bottom: 200px;
  text-align: center;
}
.button button{
  background-color: orange;
  border-radius: 10px;
  font-size: 15px;
}
</style>
