<script>

import axios from 'axios'
import { reactive, ref } from 'vue'
import { jsx } from 'vue/jsx-runtime';

export default {
  data(){
    return{
      articles:
      [ { "userId": 1, "id": 1, "title": "test1", "body": "default data" },
      { "userId": 1, "id": 2, "title": "test2", "body": "default data" }],
      pageNumber: 0,

    }
  },
  props: {
    listData: {
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
    getArticles(){
      axios.get('https://jsonplaceholder.typicode.com/posts?_limit=20')
      .then(res =>{
        this.articles=res;
        console.log("AAAAAA");});

    },
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
  // return articles.slice(start, end);
  return this.articles
        .slice(start, end);
        
},


  },
  computed:{

},
  mounted(){
 // getArticles();
 axios.get('https://jsonplaceholder.typicode.com/posts?_limit=20')
.then(res =>{
  this.articles=res.data;
  console.log("AAAAAA");
});

 
}

}


// var dataURL = 'https://jsonplaceholder.typicode.com/posts?_limit=20';

// const size = 3
// // let pageNumber = 0

// let counter = reactive({
//   pageNumber: 0
// })

// let articles = 
// [ { "userId": 1, "id": 1, "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit", "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto" },
//  { "userId": 1, "id": 2, "title": "qui est esse", "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla" }
// ]



// function mounted(){
//   // var self = this //?
//   //axios plugin

//   $.getJSON(dataURL, function (data) {
//     articles = data;
    
//   });
// //  return articles;
//   // axios.get('https://jsonplaceholder.typicode.com/posts?_limit=20')
// // .then(res =>(articles));

// }
// mounted()



// function nextPage() {
//   counter.pageNumber++;
// }
// function prevPage() {
//   counter.pageNumber--;
// }

// function selectPage(page) {
//   counter.pageNumber = page;
// }

// function pageCount() {
//   let l = articles.length,
//     s = size;
//   return Math.ceil(l / s);
// }

// function paginatedData() {
//   const start = counter.pageNumber * size,
//     end = start + size;
//   // return articles.slice(start, end);
//   return articles
//         .slice(start, end);
//         //nn
// }


</script>


<template>
  <div>
    <!-- <p>{{ articles }}</p> -->

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
