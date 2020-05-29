<template>
  <div id="app" class="flex flex-col">
    <img src="./assets/logo.png" style="height: 300px; width: 200px">
    <h1 class="text-6xl text-white grid-cols-1 p-10">MAGIC THE GATHERING</h1>
    <search class="object-center"></search>
    <card-profile></card-profile>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import CardProfile from './components/CardProfile.vue'

export default {
  name: 'App',
  components: {
    Search: Search,
    CardProfile: CardProfile
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  align-items: center;
  color: #2c3e50;
  margin-top: 60px;
  /* test */
}
</style>
