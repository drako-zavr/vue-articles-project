<script setup>
import NewArticle from './components/NewArticle.vue'
import Articles from './components/Articles.vue'
import axios from 'axios'

</script>
<script>

 
export default {
  data(){
    return{
      articles:
      [ { "userId": 1, "id": 1, "title": "AAAA", "body": "default data" },
      { "userId": 1, "id": 2, "title": "AAAA", "body": "default data" }],
      pageNumber: 0,
      title:'',
      body:''

    }
  },

  methods: {
    addArticle(newtitle, newbody) {
      if (this.title != '' && this.body != '') {
        this.articles.push({
          title: newtitle,
          body: newbody
        });
      };

  this.title = '';
  this.body = '';
},
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
  
  <form id="articleform" class="article-form" v-on:submit.prevent="addArticle(title, body)">
    <input name="title" id="title" ref="inputtitle" class="article-form__input" type="text"
      placeholder="Введите Название статьи" v-model="title">
    <input name="body" id="body" class="article-form__input" type="text" placeholder="Введите Основной текст"
      v-model="body">
    <button id="createarticle" type="submit" class="article-form__button">Добавить новую статью</button>
  </form>

  <!-- <NewArticle /> -->
  <h1>Статьи</h1>

  <Articles :articles="articles" ></Articles>

</template>

<style scoped>
</style>
