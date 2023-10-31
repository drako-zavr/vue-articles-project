<script>

import axios from 'axios'
import { reactive, ref } from 'vue'
import { jsx } from 'vue/jsx-runtime';


export default {
  data(){
    return{
    //   articles:
    //   [ 
    //   //   { "userId": 1, "id": 1, "title": "test1", "body": "default data" },
    //   // { "userId": 1, "id": 2, "title": "test2", "body": "default data" }
    // ],
      pageNumber: 0,
    }
  },
  props: {
    articles: {
      type: Array,
      required: true
    },
    size: {
      type: Number,
      required: false,
      default: 6
    }
  },
  methods: {
    nextPage() {
      this.pageNumber++;
    },
    prevPage() {
      this.pageNumber--;
    },
    selectPage(page) {
      this.pageNumber = page;
    },
    pageCount() {
      let l = this.articles.length,
      s = this.size;
      return Math.ceil(l / s);
    },
    paginatedData() {
      const start = this.pageNumber * this.size,
      end = start + this.size;
      return this.articles
        .slice(start, end);
      },

  },
  computed:{
   //?
    },
  
}

</script>


<template>
  <div>

    <div v-for="p in paginatedData()">

      <div class="article col">
        <h3 class="title">{{ p.title }}</h3>
        <p class="body">{{ p.body }}</p>
      </div>

    </div> 

    <div class="pagination">

      <button class="pagination__button" :disabled="pageNumber === 0" @click="prevPage">
        &#60;&#60;
      </button>

      <div v-for="a in pageCount()" >
        <button class="pagination__button" @click="selectPage(a-1)">{{ a }}</button>
      </div>

      <button class="pagination__button " :disabled="pageNumber >= pageCount() - 1" @click="nextPage">
        &#62;&#62;
      </button>
    
    </div>

  </div>

</template>
