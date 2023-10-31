<script>



export default{
  data() {
    return {
      title :'',
      body : '',
    }
  },


}
 

</script>

<template>

  <form id="articleform" class="article-form" v-on:submit.prevent="addArticle(title, body)">
    <input name="title" id="title" ref="inputtitle" class="article-form__input" type="text"
      placeholder="Введите Название статьи" v-model="title">
    <input name="body" id="body" class="article-form__input" type="text" placeholder="Введите Основной текст"
      v-model="body">
    <button id="createarticle" type="submit" class="article-form__button">Добавить новую статью</button>
  </form>

</template>

<style scoped></style>
