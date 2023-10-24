<script setup>
// defineProps({
//   arr: {
//     type: Array,
//     required: true
//   }
// })

import { reactive, ref } from 'vue'




var dataURL = 'https://jsonplaceholder.typicode.com/posts?_limit=20';
const size = 3
// let pageNumber = 0

let counter = reactive({
  pageNumber: 0
})

let articles = 
[ { "userId": 1, "id": 1, "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit", "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto" },
 { "userId": 1, "id": 2, "title": "qui est esse", "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla" }
]



function mounted(){
  // var self = this //?
  $.getJSON(dataURL, function (data) {
    articles = data;
    
    
  });
  return articles;

}
mounted()
// (async function() {
//   await mounted();
//   // other things after script loaded
// })();



function nextPage() {
  counter.pageNumber++;
}
function prevPage() {
  counter.pageNumber--;
}

function selectPage(page) {
  counter.pageNumber = page;
}

function pageCount() {
  let l = articles.length,
    s = size;
  return Math.ceil(l / s);
}

function paginatedData() {
  const start = counter.pageNumber * size,
    end = start + size;
  // return articles.slice(start, end);
  return articles
        .slice(start, end);
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

      <button class="pagination__button" :disabled="counter.pageNumber === 0" @click="prevPage">
        &#60;&#60;
      </button>


      <div v-for="a in pageCount()">
        <button class="pagination__button" @click="selectPage(a)">{{ a }}</button>
      </div>

      <button class="pagination__button" :disabled="counter.pageNumber >= pageCount() - 1" @click="nextPage">
        &#62;&#62;
      </button>
      <!-- <button class="pagination__button" @click="articles.push({
      title: 'newtitle',
      body: 'newbody'
    })"></button> -->
<!-- <p>counter.pageNumber = {{ counter.pageNumber }}</p>
<p>{{ articles}}</p>
<p>pageCount = {{ pageCount() }}</p>
<p>paginatedData {{ paginatedData()}}</p> -->
<!-- <p>mounted() {{ mounted() }}</p> -->

    </div>

  </div>



</template>
