<template>
  <h1 class="adventureListHeader">Adventure Works Category List</h1>
  <ul v-show="fetchComplete" id="categoryList">
  </ul>
  <h1 v-show="!fetchComplete">Waiting for fetch</h1>
  <button v-on:click="test">Click</button>
</template>

<script>
const VCategoryList = {
  data(){
    return{
       fetchComplete:false,
       users:[],
    }
  },
  methods:{
    fetch(){
      const list = document.getElementById('categoryList')
      
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(json => {
          this.fetchComplete = true;
          return json.map(e => {
            let element = document.createElement('li')
            element.innerText = e.name;
            return element;
          })
        })
        .then((elements) => {
          this.users = elements;
          list.append(...elements)
        })

      }
  },
  mounted(){
    this.fetch();
  },
  updated(){
    console.log(this.users)
  }
}
export default VCategoryList;
</script>

<style scoped>
  
</style>
