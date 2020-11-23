<template>
  <div class="all">
    <div class="container">
      <movie-index-header></movie-index-header>
      <user-message></user-message>
      <div class="main">
        <movie-show style="margin-top: 4px" v-bind:movie-items="movieItems"></movie-show>
        <div class="newList">
          <div class="newListTitle">
            <p>📰新闻</p>
          </div>
          <ul>
            <news-list v-for="item in newsItems"
                       :key="item._id"
                       :id="item._id"
                       :articleTitle="item.articleTitle"
                       :articleTime="item.articleTime">
            </news-list>
          </ul>
        </div>
      </div>
    </div>
    <div>
      <common-footer></common-footer>
    </div>
  </div>
</template>

<script>
import MovieIndexHeader from '../components/MovieIndexHeader'
import UserMessage from "../components/UserMessage";
import MoviesList from '../components/MoviesList'
import MovieShow from "../components/MovieShow";
import NewsList from '../components/NewsList'
import CommonFooter from '../components/commonFooter'

export default {
  name: "index",
  data(){
    return {
      headerItems: [],
      newsItems: [],
      movieItems: [],
    }
  },
  components: {
    UserMessage,
    MovieIndexHeader,
    MoviesList,
    MovieShow,
    NewsList,
    CommonFooter,
  },
  //  这里用于获取数据，需要获得主页推荐，主页新闻列表，主页电影列表
  created () {
// 主页推荐
    this.$http.get('http://localhost:3000/showIndex').then((data) => {
      this.headerItems = data.body.data
    })
//    获取新闻
    this.$http.get('http://localhost:3000/showArticle').then((data) => {
      this.newsItems = data.body.data
    })
//   获取所有电影
    this.$http.get('http://localhost:3000/showRanking').then((data) => {
      this.movieItems = data.body.data
      console.log(this.movieItems);
    })
  },
  updated() {
    console.log(this.movieItems);
  },
}
</script>

<style scoped>
.container{
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.newList{
  width: 25%;
  height: 100%;
}
.newListTitle{
  margin: 0 auto;
  height: 30px;
  text-align: center;
  font-size: 18px;
  color: #ffffff;
}
.main{
  display: flex;
  justify-content: flex-start;
}
</style>
