<template >
    <div class="dialogWrapper" v-show="isCreateDialogOpen">
    <div class="dialog">
        <h4>Add new Category</h4>
        <form action="#" @submit='submit'>
            <div class="inputWrapper">
                <label for="id">Category ID</label>
                <input type="text" name="id" id="id" disabled :placeholder="categoriesLength">
            </div>
            <div class="inputWrapper">
                <label for="name">Category Name</label>
                <input type="text" name="name" id="name" required :value="categoryName" @change="onChange" @keyup.enter="addSubcategory">
            </div>
            <div class="inputWrapper">
                <label for="subcategory">Subcategories</label>
                <ul class="newSubcategoryList"></ul>
                <input type="button" value="Add subcategory" id="addCategoryBtn" v-on:click="addSubcategory">
            </div>
            <input type="submit" value="Add Category" >
        </form>
    </div>
    <div class="backdrop" @click="$emit('openCategoryDialog',false)"></div>
    </div>
</template>

<script lang="ts">
const VCreateCategoryDialog = {
    name:"VCreateCategoryDialog",
    props:['isCreateDialogOpen','categoriesLength'],
    emits: ["openCategoryDialog"],
    data(){
        return {
            categoryName: '',
            products:[]
        }
    },
    methods:{

        addSubcategory(){
            const subcategoryLabel = document.querySelector('label[for="subcategory"]')
            const newSubcategoryList = document.querySelector('.newSubcategoryList')
            
            const newSubcategory = document.createElement('li');
            newSubcategory.classList.toggle('newSubcategory')
            
            const newSubcategoryInput = document.createElement('input');
            newSubcategoryInput.setAttribute('type','text')
            newSubcategoryInput.setAttribute('name','newSubcategory')
            newSubcategoryInput.setAttribute('required','true')

            const newSubcategoryButton = document.createElement('a');
            newSubcategoryButton.innerText = 'X';
            
            newSubcategory.append(newSubcategoryInput,newSubcategoryButton);

            newSubcategoryList.appendChild(newSubcategory)
            subcategoryLabel.insertAdjacentElement('afterEnd',newSubcategoryList)
        },
        canAddNewSubcategory(){
            const newSubcategoryInput = document.querySelector('input[name="newSubcategory"]')
            const addCategoryBtn = document.getElementById('addCategoryBtn');

            if(!newSubcategoryInput){
                return;
            }

            if(!newSubcategoryInput.value){
                addCategoryBtn.disabled = true;    
            }else{
                addCategoryBtn.disabled = false;
            }
        },
        onChange(event){
            this.categoryName = event.target.value
        },
        submit(event){
            event.preventDefault();
            //finish
            this.$emit('openCategoryDialog',false)
        }

    },
    updated(){

    }
}

export default VCreateCategoryDialog;
</script>

<style>
    .dialogWrapper{
        position:fixed;
        inset:0;
    }
    .backdrop{
        position: fixed;
        inset:0;
        background: black;
        z-index: 1;
        opacity: .6;
    }
    .dialog{
        position:fixed;
        background:white;
        padding:2em;
        z-index:2;
        overflow:auto;
        display:flex;
        align-items: center;
        flex-direction:column;
        max-height:80vh;
        inset:10%;
    }

    .inputWrapper{
        margin:20px 0px;
        padding:1em 3em;
        padding-left: 1em;
        display:flex;
        flex-direction:column;
        border:1px solid black;
        border-radius: 10px;
    }
    .inputWrapper *{
        display:block;
    }
    .inputWrapper label{
        margin-bottom:10px;
    }

    .inputWrapper .newSubcategory{
        list-style-type: none;
        display:flex;
        justify-content: space-around;
        align-items: center;
    }

    .inputWrapper .newSubcategory a{
        padding:10px;
    }

    form input {
        padding: 10px
    }
    form{
        display:flex;
        flex-direction: column;
        align-items:stretch;
    }
</style>