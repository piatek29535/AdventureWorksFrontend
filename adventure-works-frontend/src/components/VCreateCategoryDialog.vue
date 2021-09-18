<template >
    <div v-show="isCreateDialogOpen">
        
    <div class="dialog">
        <h4>Add new Category</h4>
        <form action="#">
            <label for="id">Category ID</label>
            <input type="text" name="id" id="id" disabled>
            <label for="name">Category Name</label>
            <input type="text" name="name" id="name" required>
            <label for="subcategory">Subcategories</label>
            <ul class="newSubcategoryList"></ul>
            <input type="button" value="Add subcategory" id="addCategoryBtn" v-on:click="addSubcategory">
            <input type="submit" value="Add Category">
        </form>
    </div>
    <div class="backdrop" @click="$emit('openCategoryDialog',false)"></div>
    
</div>
</template>

<script>
const VCreateCategoryDialog = {
    name:"VCreateCategoryDialog",
    props:['isCreateDialogOpen'],
    data(){
        return {
            dialogShow:false,
            categoryId:Math.random(1,10),
            categoryName: '' || "Test",
        }
    },
    methods:{
        toggleDialog(){
            this.show=!this.show;
        },
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
        }
        
    },
    mounted(){
    },

}

export default VCreateCategoryDialog;
</script>

<style>
    .backdrop{
        position: fixed;
        inset:0;
        background: black;
        z-index: 1;
        opacity: .6;
    }
    .dialog{
        position: fixed;
        inset: 10% 25%;
        background-color:lightgray;
        padding: 0 5em;
        overflow: auto;
        z-index: 2;
        box-shadow: -5px 5px 5px darkgray;
    }
    
    .dialog h4{
        margin: 1em;
        text-align: center;
    }
    form{
        display: flex;
        flex-direction: column;
    }
    form *{
        padding:.5em 0
    }
    form label{
        margin-top: 1em;
    }
    form:last-child{
        margin-bottom: 3em;
    }
    #addCategoryBtn{
        margin-top: 1em;
        outline:1px solid blue;
    }
    .newSubcategory{
        display:flex;
        justify-content: space-around;
        align-items: stretch;
    }
    .newSubcategory input{
        flex:8
    }
    .newSubcategory a{
        flex:1;
        border: none;
        display:block;
        cursor: pointer;
        text-align: center;
    }

</style>