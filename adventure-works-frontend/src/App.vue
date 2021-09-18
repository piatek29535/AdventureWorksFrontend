<template>
  <VCategoryList/>
</template>

<script>
import VCategoryList from './components/VCategoryList.vue'

export default {
  name: 'App',
  components: {
    VCategoryList,
  }
}
</script>

<style>
:root{
  --lightSalmon:lightsalmon;
  --white:white;
}

*,*::before,*::after{
  margin:0;
  padding:0;
  box-sizing:border-box;

}
#app {
  margin:0 auto;
  max-width:1000px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.flex{
  display:flex;
  justify-content:center;
  align-items:center;
  flex-direction:column;
}
</style>
