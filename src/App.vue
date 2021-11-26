<template>
  <div id="app">
    <product-view :data="mockUpData"/>
  </div>
</template>

<script>
import mockUpData from './mock-up-data.json'
import ProductView from "./components/ProductView";
export default {
  name: 'App',
  components: {
    'product-view': ProductView
  },
  created() {
  },
  data:()=>({
    mockUpData,
  }),
  computed: {

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 200px;
  justify-content: center;
}
</style>
