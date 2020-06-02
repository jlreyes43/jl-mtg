<template>
  <div id="app" class="flex flex-col">
    <img src="./assets/logo.png" style="height: 300px; width: 200px">
    <br>
    <img src="./assets/mtg-logo.png" style="height: 200px; width: 600px">
    <br><br>
    <div class="flex flex-row">
      <search 
        class="object-center"
        @cardProfileSearch="cardProfileSearchName = $event"></search>
      <hr>
      <card-profile
        :cardProfileSearchName = "cardProfileSearchName"></card-profile>
    </div>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import CardProfile from './components/CardProfile.vue'

export default {
  name: 'App',
  data(){
    return{
      cardProfileSearchName: ''
    }
  },
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
