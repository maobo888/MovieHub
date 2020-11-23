<template lang="html">
  <div class="container">
    <div>
      <movie-index-header ></movie-index-header>   <!--  展示引入的header组件 -->
    </div>
    <div class="contentMain">
      <h1>{{detail.articleTitle}}</h1>
      <div style="color: rgba(255,255,255,0.77)">{{detail.articleTime}}</div><br>
      <div class="contentText">
        <p>{{detail.articleContext}}</p>
      </div>
      <br>
      <hr>
      <comment v-bind:movie_id="article_id"></comment>
    </div>
    <div>
      <common-footer></common-footer>  <!--  展示引入的footer组件 -->
    </div>
  </div>
</template>
<script>
import MovieIndexHeader from '../components/MovieIndexHeader'
import CommonFooter from '../components/commonFooter'
import Comment from '../components/Comment.vue'

let article_id=0
export default {
  name: 'NewDetail',
  data () {
    return {
      detail: [],
      article_id:'',
    }
  },
  components: {
    MovieIndexHeader,
    CommonFooter,
    Comment,
  },

//  这里用于获取数据，需要获得主页推荐，主页新闻列表，主页电影列表
  created () {
//    this.$route.query.id
    article_id=this.$route.query.id
    this.article_id=article_id
    this.$http.post('http://localhost:3000/articleDetail',{article_id: article_id}).then((data) => {
      this.detail = data.body.data[0];
      this.detail.articleTime = new Date(parseInt(this.detail.articleTime)).toLocaleString();
//      console.log( data.body.data)
    })
  },
  methods:{
  }
}
</script>

<style lang="css" scoped>
.container{
  width: 1200px;
  /*height: 100vh;*/
  margin: 0 auto;
  overflow: hidden;
  font-family:"Microsoft YaHei UI"
}
.contentMain{
  width: 66%;
  margin: 0 auto;
  background-color: rgba(0, 0, 0, 0.6);
}
.contentText p{
  text-indent:2em;/*首行缩进两个单位*/
  line-height: 1.5em;/*行距为1.5个单位*/
  letter-spacing:0.02em;
  padding:10px;/*用内边距代替外边距来设置段间距*/
  margin:0;/*去掉默认的段间距*/
}
</style>
