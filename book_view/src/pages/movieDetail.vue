<template lang="html">
  <div class="container">
    <movie-index-header></movie-index-header>
    <user-message></user-message>
    <div class="contentMain">
      <div class="movieShow">
        <div class="movieName">
          <h1>{{ detail.movieName }}</h1>
        </div>
        <div class="movieImg">
          <img v-bind:src=detail.movieImg>
        </div>
        <div class="Support">
          点赞次数： {{ detail.movieNumSuppose }}
          <button v-on:click="support()" style="width: 60px">点赞👍</button>
        </div>
        <div class="download">
          下载次数： {{ detail.movieNumDownload }}
          <button v-on:click=movieDownload() style="width: 60px">下载👌</button>
        </div>
      </div>
      <comment class="comment" v-bind:movie_id="movie_id"></comment>
    </div>
    <common-footer></common-footer>
  </div>
</template>
<script>
import MovieIndexHeader from '../components/MovieIndexHeader'
import UserMessage from "../components/UserMessage"
import CommonFooter from '../components/commonFooter'
import Comment from '../components/Comment.vue'

let movie_id = 0
export default {
  name: 'MovieDetail',
  data() {
    return {
      detail: [],
      movie_id: '',
    }
  },
  components: {
    MovieIndexHeader,
    UserMessage,
    CommonFooter,
    Comment,
  },

//  这里用于获取数据，需要获得主页推荐，主页新闻列表，主页电影列表
  created() {
//    this.$route.query.id
    this.movie_id = this.$route.query.id
    movie_id = this.$route.query.id
    this.$http.post('http://localhost:3000/movie/detail', {id: movie_id}).then((data) => {
      this.detail = data.body.data;
//      console.log( data.body.data)
    })
  },
  methods: {
    support: function (event) {
      this.$http.post('http://localhost:3000/movie/support', {id: movie_id}).then((data1) => {
        let data_temp = data1.body
        let that = this
        console.log(data_temp)
        if (data_temp.status === 0) {
          this.$http.post('http://localhost:3000/movie/showNumber', {id: movie_id}).then((data2) => {
//            console.log(data2)
            that.detail['movieNumSuppose'] = data2.body.data.movieNumSuppose
          })
        } else {
          alert(data_temp.message)
        }

      })
    },
//    电影下载
    movieDownload: function (event) {
      this.$http.post('http://localhost:3000/movie/download', {movie_id: movie_id}).then((data1) => {
        if (data1.status == 1) {
          alert(data1.message)
        } else {
//          console.log(data1.data)
          window.location = data1.data;
        }
      })
    }
  }
}
</script>

<style lang="css" scoped>
.container {
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.contentMain {
  width: 800px;
  margin: 0 auto;
  text-align: center;
  display: flex;
  justify-content: flex-start;
  padding: 5px;
  border: 2px solid lightseagreen;
  border-radius: 5px;
}
.movieShow{
  width: 50%;
  border-right: 2px solid lightseagreen;
}
.movieName {

}
.movieImg img{
  width: 300px;
  height: 455px;
}
.Support{
  width: 300px;
  margin: 5px auto;
  text-align: left;
  display: flex;
  justify-content: space-between;
}
.download{
  width: 300px;
  margin: 5px auto;
  text-align: left;
  display: flex;
  justify-content: space-between;
}
.comment{
  width: 50%;
}
</style>
