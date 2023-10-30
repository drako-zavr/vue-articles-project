<script setup>
// import Articles from './Articles.vue';
 import App from '../App.vue';

let title = '';
let body = '';

function addArticle(newtitle, newbody) {
  if (title != '' && body != '') {
    App.articles.push({
      title: newtitle,
      body: newbody
    });
  };
 

  title = '';
  body = '';
};


</script>

<template>
  <!-- <p>a{{ articles.articles }}</p> -->
  <form id="articleform" class="article-form" v-on:submit.prevent="addArticle(title, body)">
    <input name="title" id="title" ref="inputtitle" class="article-form__input" type="text"
      placeholder="Введите Название статьи" v-model="title">
    <input name="body" id="body" class="article-form__input" type="text" placeholder="Введите Основной текст"
      v-model="body">
    <button id="createarticle" type="submit" class="article-form__button">Добавить новую статью</button>
  </form>
</template>

<style scoped></style>
