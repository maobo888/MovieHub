<template lang="html">
  <div class="Comment">
    <label>评论</label>
    <div class="allComment">
      <li v-for="item in items"
          style="padding-top: 3px;
          border-bottom: #20b2aa dashed 1px;
          list-style:square">
        [{{item.username}}]： {{item.context}}
      </li>
    </div>
    <div class="comment-text">
      <textarea class="textarea-inherit" v-model="context" placeholder="内容"></textarea>
    </div>
    <div class="addComment">
      <button v-on:click="send_comment">评论</button>
    </div>
  </div>

</template>
<!--这里获取所有的评论，并且可以进行评论,对于文章详情页也可以使用-->
<script>

export default {
  props: ['movie_id'],
  data() {
    return {
      items: [],
      context: '',
    }
  },
  created() {
//    获得所有的评论
//    console.log(this.movie_id)
    this.$http.post('http://localhost:3000/movie/comment', {id: this.movie_id})
      .then((data) => {
      if (data.body.status == 0) {
        this.items = data.body.data
      } else {
        alert("获得失败")
      }
    })
  },
  methods: {
    send_comment(event) {
      let send_data;
      if (typeof (localStorage.username) != "undefined") {
        send_data = {
          movie_id: this.movie_id,
          context: this.context,
          username: localStorage.username
        }
      } else {
        send_data = {
          movie_id: this.movie_id,
          context: this.context,
        }
      }
      this.$http.post('http://localhost:3000/users/postComment', send_data).then((data) => {
        alert(data.body.message)
        location.reload()
      })
    }
  }
}
</script>
<style lang="css" scoped>
.Comment{

}
.allComment{
  padding: 10px;
  text-align: left;
}
.comment-text{
  width: 379px;
  padding: 10px;
  text-align: left;
}
.textarea-inherit {
  width: 100%;
  height: 110px;
  word-break: break-all;
  resize: none;
}
.addComment{

}
</style>
