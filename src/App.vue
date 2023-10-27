<script setup>
import NewArrticle from './components/NewArticle.vue'
import Articles from './components/Articles.vue'
import axios from 'axios'
var dataURL = 'https://jsonplaceholder.typicode.com/posts?_limit=20';

let articles1 = []
// function mounted(){
//   // var self = this //?
//   $.getJSON(dataURL, function (data) {
//     articles = data;
//   });
// }

axios.get('https://jsonplaceholder.typicode.com/posts?_limit=20')
      .then(res =>{
        articles1=res;
        console.log("axios");});
</script>

<template>

  <img class="logo" src="src/assets/logo1.svg" alt="">
  <p>{{ articles }}</p>

  <NewArrticle />
  <h1>Статьи</h1>
  <Articles list-data="articles1"/>

</template>

<style scoped>
</style>
