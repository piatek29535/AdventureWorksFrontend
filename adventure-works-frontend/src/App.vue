<template>
  <VCategoryList/>
</template>

<script>
import VCategoryList from './components/VCategoryList.vue'

export default {
  name: 'App',
  components: {
    VCategoryList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
