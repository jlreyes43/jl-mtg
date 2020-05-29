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
        <div v-for="(result, index) in results" class="text-white text-left" @click="cardSelected(index)">
          <p>{{result}}</p>
        </div>
      </div>
      <div v-else class="p-20 text-white text-left">
        No results!
      </div>
    </div>

    <!-- card details -->

    <div v-if="this.hasSearched" class="text-white text-left">
      <p>Card Name: {{cardName}}</p>
      <p>Card ID: {{cardID}}</p>
      <p>Artist Name: {{artistName}}</p>
      <p>Booster: {{isBooster}}</p>
      <p>Collector Number: {{collectorNumber}}</p>
      <img :src="imageLink"/>
      <p>Release Date: {{releaseDate}}</p>
      <p>Set Name: {{setName}}</p>
      <p>EUR Price: {{this.prices.eur}}</p>
      <p>Tix Price: {{this.prices.tix}}</p>
      <p>USD Price: {{this.prices.usd}}</p>
      <p>USD Foil Price: {{this.prices.usdFoil}}</p>
      <p>Set Link: <a :href="setLink">Click Me! (Doesn't Work Yet)</a></p>
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

      // Card Details

      cardName: '',
      cardID: '',
      artistName: '',
      isBooster: '',
      collectorNumber: '',
      imageLink: '',
      releaseDate: '',
      setName: '',
      setLink: '',
      prices: {
        eur: '',
        tix: '',
        usd: '',
        usdFoil: ''
      }

    }
  },
  methods:{
    search(){
      this.hasSearched = false
      axios.get(`https://api.scryfall.com/cards/autocomplete?q=${this.query}`)
        .then(res => {
          this.results = res.data.data
        })
        .catch(error => console.log(error))

    },
    cardSelected(index){

      this.hasSearched = true
      axios.get(`https://api.scryfall.com/cards/named?exact=${this.results[index].replace(/ /g,"+")}`)
        .then(res => {
          console.log(res.data)
          this.cardName = res.data.name
          this.cardID = res.data.id
          this.artistName = res.data.artist
          this.isBooster = res.data.booster
          this.collectorNumber = res.data.collector_number
          this.imageLink = res.data.image_uris.normal
          this.releaseDate = res.data.released_at
          this.setName = res.data.set_name
          //this.setLink = res.data.set_uri
          this.prices.eur = res.data.prices.eur
          this.prices.tix = res.data.prices.tix
          this.prices.usd = res.data.prices.usd
          this.prices.usdFoil = res.data.prices.usd_foil

        })
        .catch(error => console.log(error))
    }
  },
  computed:{
    ToUpper(){
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
