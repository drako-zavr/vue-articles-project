<script setup>
import NewArticle from './components/NewArticle.vue'
import Articles from './components/Articles.vue'
import axios from 'axios'
//var dataURL = 'https://jsonplaceholder.typicode.com/posts?_limit=20';
</script>
<script>

export default {
  data(){
    return{
      articles:
      [ { "userId": 1, "id": 1, "title": "AAAA", "body": "default data" },
      { "userId": 1, "id": 2, "title": "AAAA", "body": "default data" }],
      pageNumber: 0,

    }
  },
  props: {
    listData: {
      type: Array,
      //required: true
    },
    size: {
      type: Number,
      required: false,
      default: 6
    }
  },
 
  mounted(){
    axios.get('https://jsonplaceholder.typicode.com/posts?_limit=20')
    .then(res =>{
      this.articles=res.data;
    });
  }

}
</script>

<template>

  <img class="logo" src="src/assets/logo1.svg" alt="">
  <!-- <p>b{{ articles }}</p> -->


  <NewArticle />
  <h1>Статьи</h1>

  <Articles :articles="articles"></Articles>

</template>

<style scoped>
</style>
