<template>
  <div class="w-full max-w-xl">
    
    <!-- form div -->
    <form>
      <div class="mb-4">
        <input 
          class="rounded w-full py-2 px-3 text-gray-700 focus:outline-none focus:shadow-outline" 
          type="text" 
          placeholder="Search"
          v-model="query">
      </div>
      <button 
        class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" 
        type="submit"
        @click.prevent="search">
        Search
      </button>
    </form> 
    
    <!-- results div -->
    <div class="mb-">
      <div v-if="results.length" class="p-20">
        <p v-for="(result, index) in results" class="text-white" @onclick="cardSelected">
          {{result}}
        </p>
      </div>
      <div v-else class="p-20 text-white">
        No results!
      </div>
    </div>

    <!-- card details -->

  </div>
</template>

<script>
import axios from 'axios';

export default {
  data () {
    return {
      query: '',
      results: ['']
    }
  },
  methods:{
    search(){
      axios.get(`https://api.scryfall.com/cards/autocomplete?q=${this.query}`)
        .then(res => {
          this.results = res.data.data
        })
        .catch(error => console.log(error))
    },
    cardSelected(){

      console.log(index)

      // axios.get(`https://api.scryfall.com/cards/named?exact=aust+com`)
      //   .then(res => {
      //     this.results = res.data.data
      //   })
      //   .catch(error => console.log(error))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
