<template>
  <div class="adminPage">
    <movie-index-header></movie-index-header>
    <user-message></user-message>
    <div class="main">
      <div class="movie">
        <div class="showAllMovie" style="width: 33%;">
          <h3>显示所有电影</h3>
          <ul>
            <li v-for="item in allMovie">{{item.movieName}}</li>
          </ul>
          <br>
          <button v-on:click="showAllMovie">showAllMovie</button>
        </div>
        <div class="addMovie" style="width: 33%;">
          <h3>添加电影</h3><br>
          电影名称: <input type="text" v-model="movieName" placeholder="电影名称"><br>
          电影图片地址: <input type="text" v-model="movieImg" placeholder="电影图片地址"><br>
          电影下载地址: <input type="text" v-model="movieDownload" placeholder="电影下载地址"><br>
          是否在首页展示：
          <input type="radio" name="movieMainPage" value="true" @click="getRadioVal">是
          <input type="radio" name="movieMainPage" value="" @click="getRadioVal">否<br>
          <button v-on:click="addMovie">添加</button>
        </div>
        <div class="deleteMovie" style="width: 33%;">
          <h3>删除电影</h3>
          <input type="text" v-model="movieName" placeholder="电影名称">
          <button v-on:click="deleteMovie">删除</button>
        </div>
      </div>
      <div class="comment">
        <div class="showAllComment" style="width: 33%;">
          <h3>显示评论电影</h3>
          <ul>
            <li v-for="item in allComment">
              评论id: {{item._id}}<br>
              电影id: {{item.movie_id}}<br>
              评论内容: {{item.context}}<br>
              是否通过审核: {{item.check}}</li>
          </ul>
          <button v-on:click="showAllComment">showAllComment</button>
        </div>
        <div  style="width: 33%;">
          <h3>审核电影评论</h3>
        </div>
        <div style="width: 33%;">
          <h3>删除用户评论</h3>
          <input type="text" v-model="commentId" placeholder="评论id">
          <button v-on:click="deleteComment">deleteComment</button>
        </div>
      </div>
      <div class="user">
        <div class="showAllUser"  style="width: 25%;">
          <h3>显示所有用户</h3>
          <ul>
            <li v-for="item in allUser">
              用户名：{{item.username}}<br>
              密码： {{item.password}}<br>
              邮箱： {{item.userMail}}<br>
              手机： {{item.userPhone}}<br>
              管理员权限： {{item.userAdmin}}<br>
              是否封号： {{item.userStop}}<br>
            </li>
          </ul>
          <button v-on:click="showAllUser">showAllUser</button>
        </div>
        <div  style="width: 25%;">
          <h3>添加用户管理权限</h3>
          <input type="text" v-model="userId" placeholder="用户id">
          <button v-on:click="powerUpdate">powerUpdate</button>
        </div>
        <div  style="width: 25%;">
          <h3>停封用户</h3>
          <input type="text" v-model="userId" placeholder="用户id">
          <button v-on:click="stopUser">stopUser</button>
        </div>
        <div  style="width: 25%;">
          <h3>密码修改</h3>
          <input type="text" v-model="userId" placeholder="用户id">
          <input type="text" v-model="newPassword" placeholder="新密码">
          <button v-on:click="changeUser">changeUser</button>
        </div>
      </div>
      <div class="article">
        <div class="addArticle" style="width: 75%">
          <h3>添加文章</h3>
          <input type="text" v-model="articleTitle" placeholder="文章标题"><br>
          <textarea class="textarea-inherit" v-model="articleContext" placeholder="文章内容"></textarea><br>
          <button v-on:click="addArticle">addArticle</button>
        </div>
      </div>
    </div>
    <div class="foot"></div>
  </div>
</template>

<script>
import MovieIndexHeader from '../components/MovieIndexHeader'
import UserMessage from "../components/UserMessage";
export default {
  name: "adminPage",
  data(){
    return{
      username: '',
      token: '',
      id: '',
      movieName: '',
      movieImg: '',
      movieDownload: '',
      movieMainPage: true,
      allMovie: [],
      allComment: [],
      allUser: [],
      commentId: '',
      userId: '',
      newPassword: '',
      articleTitle: '',
      articleContext: '',
      articleId: '',
    }
  },
  components:{
    MovieIndexHeader,
    UserMessage
  },
  created() {
    this.username = localStorage.getItem('username')
    this.token = localStorage.getItem('token')
    this.id = localStorage.getItem('_id')
  },
  methods:{
    //获取input-radio的值
    getRadioVal(event){
      this.movieMainPage = event.target.value;
    },
    //添加电影
    addMovie(){
      this.$http.post('http://localhost:3000/admin/movieAdd',{
        username: this.username,
        token: this.token,
        id: this.id,
        movieName: this.movieName,
        movieImg: this.movieImg,
        movieDownload: this.movieDownload,
        movieMainPage: this.movieMainPage
      }).then((data) => {
        if(data.body.status === 1 ){
          alert(data.body.message)
        }
        else {
          alert(data.body.message)
        }
      })
    },
    deleteMovie(){
      this.$http.post('http://localhost:3000/admin/movieDel',{
        username: this.username,
        token: this.token,
        id: this.id,
        movieName: this.movieName,
      }).then((data) => {
        if(data.body.status === 1 ){
          alert(data.body.message)
        }
        else {
          alert(data.body.message)
        }
      })
    },
    showAllMovie(){
      this.$http.get('http://localhost:3000/admin/movie',)
        .then((data) => {
          this.allMovie = data.data.data.slice()
          console.log(this.allMovie);
        })
    },
    showAllComment(){
      this.$http.get('http://localhost:3000/admin/commentsList',)
        .then((data) => {
          this.allComment = data.data.data.slice()
          console.log(this.allComment);
        })
    },
    deleteComment(){
      this.$http.post('http://localhost:3000/admin/delComment',{
        username: this.username,
        token: this.token,
        id: this.id,
        commentId: this.commentId,
      }).then((data) => {alert(data.body.message)})
    },
    stopUser(){
      this.$http.post('http://localhost:3000/admin/stopUser',{
        username: this.username,
        token: this.token,
        id: this.id,
        userId: this.userId,
      }).then((data) => {alert(data.body.message)})
    },
    changeUser(){
      this.$http.post('http://localhost:3000/admin/changeUser',{
        username: this.username,
        token: this.token,
        id: this.id,
        userId: this.userId,
        newPassword: this.newPassword,
      }).then((data) => {alert(data.body.message)})
    },
    showAllUser(){
      this.$http.post('http://localhost:3000/admin/showUser',{
        username: this.username,
        token: this.token,
        id: this.id,
      }).then((data) => {
        this.allUser = data.data.data.slice()
        console.log(this.allUser);
      })
    },
    powerUpdate(){
      this.$http.post('http://localhost:3000/admin/powerUpdate',{
        username: this.username,
        token: this.token,
        id: this.id,
        userId: this.userId,
      }).then((data) => {alert(data.body.message)})
    },
    addArticle(){
      this.$http.post('http://localhost:3000/admin/addArticle',{
        username: this.username,
        token: this.token,
        id: this.id,
        articleTitle: this.articleTitle,
        articleContext: this.articleContext,
      }).then((data) => {alert(data.body.message)})
    },
    delArticle(){
      this.$http.post('http://localhost:3000/admin/delArticle',{
        username: this.username,
        token: this.token,
        id: this.id,
        articleId: this.articleId,
      }).then((data) => {alert(data.body.message)})
    },
    addRecommend(){

    },
    delRecommend(){

    }
  }
}
</script>

<style scoped>
.adminPage{
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.main{
  width: 75%;
  margin: 0 auto;
}
.movie{
  display: flex;
  justify-content: space-between;
  margin: 5px auto;
  padding: 5px;
  border: 2px solid orange;
  border-radius: 5px;
  text-align: center;
}
.comment{
  display: flex;
  justify-content: space-between;
  margin: 5px auto;
  padding: 5px;
  border: 2px solid orange;
  border-radius: 5px;
  text-align: center;
}
.user{
  display: flex;
  justify-content: space-between;
  border: 2px solid orange;
  border-radius: 5px;
  text-align: center;
  margin: 5px auto;
  padding: 5px;
}
.article{
  display: flex;
  justify-content: center;
  border: 2px solid orange;
  border-radius: 5px;
  text-align: left;
  margin: 5px auto;
  padding: 5px;
}
.textarea-inherit {
  width: 100%;
  height: 200px;
  word-break: break-all;
  resize: none;
}
.foot{
  height: 100px;
}
</style>
