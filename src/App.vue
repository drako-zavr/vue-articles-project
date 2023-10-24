<script setup>
import NewArrticle from './components/NewArticle.vue'
import Articles from './components/Articles.vue'

var dataURL = 'https://jsonplaceholder.typicode.com/posts?_limit=20';

let articles = []
// function mounted(){
//   // var self = this //?
//   $.getJSON(dataURL, function (data) {
//     articles = data;
//   });
// }
</script>

<template>

  <img class="logo" src="src/assets/logo1.svg" alt="">

  <NewArrticle />
  <h1>Статьи</h1>
  <Articles />

</template>

<style scoped>
</style>
