<template lang="html">
  <div class="container">
    <div>
      <movie-index-header></movie-index-header>   <!--  展示引入的header组件 -->
    </div>
    <div class="userMessage">
      <user-message></user-message>
    </div>
    <div class="main">
      <h3>收件箱</h3>
      <div>
        <email-list v-for="item in receive_items" :title="item.title" :fromUser="item.fromUser"
                    :context="item.context"></email-list>
      </div>
      <h3>发件箱</h3>
      <div>
        <email-list v-for="item in send_items" :title="item.title" :fromUser="item.fromUser"
                    :context="item.context"></email-list>
      </div>
      <send-talk-box></send-talk-box>
    </div>
    <common-footer></common-footer>
  </div>
</template>
<script>
import MovieIndexHeader from '../components/MovieIndexHeader'
import CommonFooter from '../components/commonFooter'
import UserMessage from '../components/UserMessage'
import EmailList from '../components/EmailList.vue'
import SendTalkBox from '../components/SendTalkBox.vue'

export default {
  name: 'HelloWorld',
  data() {
    return {
      receive_items: [],
      send_items: [],
      detail: [],
    }
  },
  components: {
    MovieIndexHeader,
    CommonFooter,
    UserMessage,
    EmailList,
    SendTalkBox,
  },

//  这里用于获取数据，需要获得主页推荐，主页新闻列表，主页电影列表
  created() {
    let userId = localStorage._id
    let send_data = {
      token: localStorage.token,
      user_id: localStorage._id,
      receive: 2
    }
    let receive_data = {
      token: localStorage.token,
      user_id: localStorage._id,
      receive: 1
    }
    if (userId) {
      this.$http.post('http://localhost:3000/users/showEmail', send_data)
        .then((data) => {
          if (data.body.status == 1) {
            alert(data.body.message)
          } else {
            this.send_items = data.body.data;
          }
          console.log(data.body.data)
        })
      this.$http.post('http://localhost:3000/users/showEmail', receive_data)
        .then((data) => {
          if (data.body.status == 1) {
            alert(data.body.message)
          } else {
            this.receive_items = data.body.data;
          }
          console.log(data.body.data)
        })
    } else {
      alert("用户信息错误")
    }
  },
  methods: {}
}
</script>

<style lang="css" scoped>
.container{
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.main{
  width: 50%;
  height: 500px;
  margin: 0 auto;
  background-color: rgba(255,255,255,0.1);
}
</style>
