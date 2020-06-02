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
    <div class="mb-" v-if="!this.hasSearched" >
      <div v-if="results.length" class="p-20">
        <div v-for="(result, index) in results" class="text-white text-left" @click="cardSelected(index); cardProfileSearchTrigger">
          <p>{{result}}</p>
        </div>
      </div>
      <div v-else class="p-20 text-white text-left">
        No results!
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data () {
    return {
      query: '',
      results: [''],
      hasSearched: false,
      
    }
  },
  props:{
    searchCardName: String
  },
  methods:{
    search(){
      this.hasSearched = false
      axios.get(`https://api.scryfall.com/cards/autocomplete?q=${this.query}`)
        .then(({data}) => {
          this.results = data.data
        })
        .catch(error => console.log(error))
    },
    cardSelected(index){
      this.hasSearched = true
      this.$emit('cardProfileSearch', this.results[index].replace(/ /g,"+"))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
