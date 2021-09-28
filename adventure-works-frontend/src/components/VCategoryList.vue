<template>
  <h1 class="adventureListHeader">Adventure Works Category List</h1>
  <ul v-show="fetchComplete" id="categoryList">
    <li @click="fetchProductList($event, category.productCategoryID)" v-for="category in categories" :key="category.id" class="category">
      <h4>{{category.name}}</h4>
        <ol class="productList hide">
            <h5>{{category.name}} product list</h5>
            <li v-for="product in products" v-bind:key='product'>
              {{product.name}}
            </li>
        </ol>
    </li>
  </ul>
  <VLoadingBar v-show="!fetchComplete"></VLoadingBar>
<VAddButton @openCategoryDialog="openCategoryDialog"/>
<VCreateCategoryDialog :isCreateDialogOpen="isCreateDialogOpen" @openCategoryDialog="openCategoryDialog"
:categoriesLength='categoriesLength'/>
</template>

<script lang="ts">
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
       categoriesLength:0,
       products: []
    }
  },
  methods:{
    fetch(){
      fetch('https://localhost:44398/categories')
        .then(response => response.json())
        .then(json => {
          this.categories = json;
          this.isCreateDialogOpen = false;
        })
        .catch(e => console.log(e))
        .finally(() => {
          this.fetchComplete = true;
        })
      },
      openCategoryDialog(value){
        if(!this.fetchComplete){
          return;
        }
        this.isCreateDialogOpen=value;
        this.categoriesLength = this.categories.length;
      },
      fetchProductList(event, CategoryID){
        this.products = []
        const productList = event.currentTarget;

        fetch(`https://localhost:44398/product/${CategoryID}`)
          .then(res => res.json())
          .then(response => {

            if(productList.classList.contains('hide')){
              productList.classList.add('show')
              productList.classList.remove('hide')
            }
            else{
              productList.classList.add('hide')
              productList.classList.remove('show')  
            }

            this.products = [...response]
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
    height:0px;
    overflow:hidden;
    transition:height .3s;
  }
  .productList{
    overflow: hidden;
    list-style-type: armenian;
  }
  .hide{
    height:0;
  }
  .show{
    height:auto;
  }

</style>
