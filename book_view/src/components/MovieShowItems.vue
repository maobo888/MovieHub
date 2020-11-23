<template>
  <div class="movieItem">
    <router-link
      :to="{path: '/movieDetail', query:{ id: movieItems._id }}">
      <div class="movieImg"><img :src="movieItems.movieImg"></div>
      <div class="movieName">{{movieItems.movieName}}</div>
    </router-link>
  </div>
</template>

<script>
export default {
  name: "MovieShowItems",
  props: ['movieItems'],
}
</script>

<style scoped>
.movieItem{
  width: 17%;
  margin: 12px;
  border: orange solid 1px;
  border-radius: 5px;
}
.movieImg{
  top: 2px;
  left: 2px;
  right: 2px;
  position: relative;
  height: 88%;
}
.movieImg img{
  width: 98%;
  height: 99%;
}
.movieName{
  position: relative;
  top: 5px;
  text-align: center;
}
a {
  color: white;
  text-decoration: none;
}
a:hover{
  color: orange;
}
</style>
