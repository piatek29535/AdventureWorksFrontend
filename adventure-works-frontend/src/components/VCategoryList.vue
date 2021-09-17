<template>
  <h1 class="adventureListHeader">Adventure Works Category List</h1>
  <ul v-show="fetchComplete" id="categoryList">
    <li v-for="category in categories" :key="category.id" class="category">
      {{category.name}}
    </li>
  </ul>
  <h1 v-show="!fetchComplete">Waiting for fetch</h1>
<VAddButton/>
</template>

<script>
import VAddButton from "./VAddButton"

const VCategoryList = {
  name:"VCategoryList",
  components:{
    VAddButton,
  },
  data(){
    return{
       fetchComplete:false,
       categories:[],
    }
  },
  methods:{
    fetch(){
      
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(json => {
          this.fetchComplete = true;
          this.categories = json;
        })
        .then((elements) => {
          this.users = elements;
        })

      }
  },
  mounted(){
    this.fetch();
  },
}
export default VCategoryList;
</script>

<style scoped>
  .adventureListHeader{
    margin-bottom:1em;
    text-align: center;
  }
  #categoryList{
    list-style-type: none;
    align-self: stretch;
  }

  #categoryList .category{
    margin:10px;
    padding:1em 3em;
    cursor:pointer;
    border:1px solid grey;
    box-shadow: 0px 0px 5px grey;
    transition: box-shadow .5s, transform .5s;
  }
  #categoryList .category:hover{
    transform:translate(5px,-5px);
    box-shadow: -10px 10px 5px grey;
  }
</style>
