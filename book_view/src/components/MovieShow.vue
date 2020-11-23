<template>
<!--  v-show="movieItems.length"movieItems更新了才渲染-->
  <div class="movieShow" v-show="movieItems.length">
    <movie-show-items class="movieShowItems"
                      v-for="item in movieItems"
                      :movieItems="item"
                      v-show="movieItems.length">
    </movie-show-items>
  </div>
</template>

<script>
import MovieShowItems from "./MovieShowItems";
export default {
  name: "MovieShow",
  components:{
    MovieShowItems,
  },
  props:['movieItems'],
  data(){
    return{

    }
  },
  methods:{

  },
  watch:{
    movieItems(newVal,oldVal){
      if(newVal){
        // console.log(this.movieItems);
      }
      else {
        // console.log('movieItems空');
      }
    }
  },
}
</script>

<style scoped>
.movieShow{
  width: 75%;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  padding: 5px;
  /*border: 2px solid orange;*/
  border-radius: 5px;
  background-color: rgba(245, 255, 255, 0.15);
}
</style>
