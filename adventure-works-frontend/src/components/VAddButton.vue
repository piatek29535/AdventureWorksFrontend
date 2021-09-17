<template>
    <button>
        Add Category
    </button>
</template>


<script>
    const VAddButton = {

    }

    export default VAddButton;
</script>

<style scoped>
    button{
        background-color:white;;
        color:lightsalmon;
        outline:none;
        padding:20px;
        position:fixed;
        right:1em;
        bottom:1em;
        border: 1px solid lightsalmon;
        border-radius:3em;
        transition:background-color .3s, color .3s, border .3s;
    }
    button:hover{
        background-color: lightsalmon;
        color:white;
        border:1px solid white;
        cursor:pointer;
    }
</style>
