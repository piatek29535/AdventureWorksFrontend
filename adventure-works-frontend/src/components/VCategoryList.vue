<template>
  <h1 class="adventureListHeader">Adventure Works Category List</h1>
  <ul id="categoryList">
  </ul>
  <button v-on:click="test">Click</button>
  <p>Cześć {{msg}}</p>
</template>

<script>
const VCategoryList = {
  data(){
    return{
       
    }
  },
  methods:{
    test(){
      const list = document.getElementById('categoryList')

      const digits = [1,2,3,4,5,6,7,8].map(i =>{
        const liElement = document.createElement('li');
        liElement.innerText = i;
        return liElement;
      });

      list.append(...digits)
    }
  }
}
export default VCategoryList;
</script>

<style scoped>
  
</style>
