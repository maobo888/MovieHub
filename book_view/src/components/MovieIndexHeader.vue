<template>
  <div class="header">
    <div style="text-align: center">
      <img src="../assets/MovieHub.png"
           height="119"
           width="405"/>
    </div>
    <div class="navigate">
      <router-link to="/" class="header_menu">
        <div>🏠主页</div>
      </router-link>
      <router-link to="/movieList" class="header_menu">
        <div>🎬全部电影</div>
      </router-link>
      <router-link to="/admin" class="header_menu">
        <div>
          👮‍♂️网站管理
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieIndexHeader",
  data(){
    return{
      isAdmin:false,
    }
  },
}
</script>

<style lang="css" scoped>
.navigate {
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: flex-start;
  text-align: center;
  background-color: orange;
  border: 2px solid black;
  border-radius: 10px;
}
.header_menu {
  width: 11.5%;
  padding-top: 20px;
  color: #fff;
  text-align: center;
}
a{
  color: white;
  text-decoration: none;
}
a:hover{
  color: greenyellow;
}
</style>
