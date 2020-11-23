<template lang="html">
  <div class="newsList">
    <li>
      <router-link :to="{path: '/newDetail', query:{ id: id }}" class="goods-list-link">  <!--  这个是用来跳转页面的，可以理解为a标签 -->
        <div>{{ articleTitle }}</div>
        <div>{{ articleTimeShow }}</div>
      </router-link>
    </li>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articleTimeShow: ''
    }
  },
  props: ['id', 'articleTitle', 'articleTime'], /*  props是子组件获取父组件数据用的 */
  created() {
    this.articleTimeShow = new Date(parseInt(this.articleTime)).toLocaleString().replace(/:\d{1,2}$/, ' ');
  }
}
</script>
<style lang="css" scoped>
.newsList {
  padding: 5px;
  font-size: 13px;
  color: orange;
  border-bottom: 1px dashed #ababab;
}
a {
  color: white;
  text-decoration: none;
}
a:hover{
  color: orange;
}
</style>
