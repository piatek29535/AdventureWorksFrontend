<template>
  <h1 class="adventureListHeader">Adventure Works Category List</h1>
  <ul v-show="fetchComplete" id="categoryList">
    <li v-on:click="test" v-for="category in categories" :key="category.id" class="category">
      <h4>{{category.name}}</h4>
      <div id="categoryListDescription">{{category.username}}</div>
    </li>
  </ul>
  <VLoadingBar v-show="!fetchComplete"></VLoadingBar>
<VAddButton @openCategoryDialog="openCategoryDialog"/>
<VCreateCategoryDialog :isCreateDialogOpen="isCreateDialogOpen" @openCategoryDialog="openCategoryDialog"/>
</template>

<script>
import VAddButton from "./VAddButton"
import VCreateCategoryDialog from "./VCreateCategoryDialog"
import VLoadingBar from "./VLoadingBar"

const VCategoryList = {
  name:"VCategoryList",
  components:{
    VAddButton,
    VCreateCategoryDialog,
    VLoadingBar
  },
  data(){
    return{
       fetchComplete:false,
       categories:[],
       isCreateDialogOpen:false,
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
        .catch((e) => {
          //Handle error 
            console.log(e)
        })

      },
      test(event){
        console.log(event)
      },
      openCategoryDialog(value){
        this.isCreateDialogOpen=value;
      }
  },
  mounted(){
    // this.fetch();
  },
}
export default VCategoryList;
</script>

<style scoped>
  .adventureListHeader{
    margin-bottom:1em;
    text-align: center;
    color:transparent;
    background: linear-gradient(to bottom, var(--lightSalmon) 90%, var(--white));
    background-clip: text;
  }
  #categoryList{
    list-style-type: none;
    align-self: stretch;
  }

  #categoryList .category{
    margin:10px;
    padding:1em 3em;
    cursor:pointer;
    border:1px solid var(--lightSalmon);
    box-shadow: 0px 0px 5px grey;
    transition: box-shadow .5s, transform .5s;
  }
  #categoryList .category:hover{
    transform:translate(5px,-5px);
    box-shadow: -10px 10px 5px var(--lightSalmon);
  }

  #categoryListDescription{
    position:relative;
    height:0.1px;
    overflow:hidden;
    transition:height .3s;
  }
  #categoryList .category:hover #categoryListDescription{
    height:100px;
  }
</style>
