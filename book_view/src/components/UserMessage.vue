<template>
  <div class="header">
    <div v-if=!isLogin class="header_item">
      <router-link to="/loginPage">
        <div class="header_text">
          😎登陆
        </div>
      </router-link>
    </div>
    <div v-else class="header_item">
      <router-link to="/userInfo">
        <div class="header_text">
          🙂已登陆: {{username}}
        </div>
      </router-link>
    </div>
    <div class="header_item">
      <button v-on:click="clear">注销</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserMessage",
  data(){
    return{
      isLogin:false,
      username:'游客'
    }
  },
  created() {
    console.log(localStorage);
    let token = localStorage.getItem('token')
    if(token){
      this.isLogin = true
      this.username = localStorage.getItem('username')
      this.id = localStorage.getItem('_id')
    }
    else {
      console.log('用户登录失败,无法获取token')
    }
  },
  methods: {
    clear () {
      localStorage.clear()
      location.reload()
    }
  }
}
</script>

<style scoped>
  .header{
    display: flex;
    justify-content: flex-end;
    width: 100%;
    height: 30px;
    background-color: orange;
    border: 2px solid black;
    border-radius: 10px;
  }
  .header_text{
    top: 50%;
    padding-right: 0px;
    padding-top: 2px;
    color: white;
  }
  .header_item{
    width: 130px;
    height: 25px;
    margin: auto 0;
  }
  a{
    text-decoration: none;
  }
</style>
