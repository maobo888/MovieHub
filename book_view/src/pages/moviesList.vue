<template lang="html">
  <!--此页面需要-->
  <div class="container">
    <div>
      <movie-index-header></movie-index-header>   <!--  展示引入的header组件 -->
      <user-message></user-message>
    </div>
    <movie-show class="contentMain" v-bind:movie-items="movieItems"></movie-show>
    <div>
      <common-footer></common-footer>
    </div>
  </div>
</template>
<script>
import MovieIndexHeader from '../components/MovieIndexHeader'
import CommonFooter from '../components/commonFooter'
import MoviesList from '../components/MoviesList'
import UserMessage from "../components/UserMessage";
import MovieShow from "../components/MovieShow";


export default {
  name: 'movieList',
  data() {
    return {
      movieItems: []
    }
  },
  components: {
    MovieIndexHeader,
    CommonFooter,
    MoviesList,
    UserMessage,
    MovieShow
  },

//  这里用于获取数据
  created() {
//    获取所有电影
    this.$http.get('http://localhost:3000/movie/list').then((data) => {
      this.movieItems = data.body.data
      console.log(data.body)
    })
  },
  methods: {}
}
</script>

<style lang="css" scoped>
.container {
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}

.contentMain {
  margin: 0 auto;
}
</style>
