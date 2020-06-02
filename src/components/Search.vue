<template>
  <div class="w-full max-w-xl">
    
    <!-- form div -->
    <form>
      <div class="mb-4 flex flex-row">
        <input 
          class="rounded w-full py-2 pl-2 pr-12 text-gray-700 focus:outline-none focus:shadow-outline" 
          type="text" 
          placeholder="Search"
          v-model="query">
        <div class="px-10">
          <button
            class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" 
            type="submit"
            @click.prevent="search">
            Search
          </button>
        </div>
      </div>
    </form> 
    
    <!-- results div -->
    <div v-if="!this.hasSearched">
      <div v-if="results.length" class="pt-5 pl-10 rounded-lg bg-gray-200">
        <div v-for="(result, index) in results" class="text-left box-border pl-2 pt-2 pb-2 pr-10" @click="cardSelected(index)">
          <p>{{result}}</p>
        </div>
      </div>
      <div v-else class="p-5 rounded-lg bg-gray-200 text-left">
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
