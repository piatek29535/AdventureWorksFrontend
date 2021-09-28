<template>
    <button @click="$emit('openCategoryDialog',true)">
        Add Category
    </button>
</template>


<script lang="ts">
    const VAddButton = {
        
    }

    export default VAddButton;
</script>

<style scoped>

    button{
        background-color:var(--lightSalmon);
        color:var(--white);
        font-weight: bold;
        outline:none;
        padding:20px;
        position:fixed;
        right:1em;
        bottom:1em;
        border: 1px solid var(--lightSalmon);
        border-radius:3em;
        transition:background-color .3s, color .3s, border .3s;
    }
    button:hover{
        background-color: var(--white);
        color:var(--lightSalmon);
        border:1px solid var(--lightSalmon);
        cursor:pointer;
    }
</style>
