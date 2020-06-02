<template>
    <div v-if="isLoaded">
        <div class="flex flex-col bg-white ml-10 rounded-lg">
            <div class="pt-5">
                <strong>Card Name: {{cardName}}</strong>
            </div>
            <div class="flex flex-row">
                <div class="p-5">
                    <img :src="imageLink" height="800px" width="320px"/>
                </div>
                <div class="text-left p-10">
                    <p>Card ID:</p> 
                    <p>{{cardID | toUpperCase}}</p>
                    <hr>
                    <p>Artist Name: {{artistName}}</p>
                    <p>Booster: {{isBooster}}</p>
                    <p>Collector Number: {{collectorNumber}}</p>
                    <p>Release Date: {{releaseDate}}</p>
                    <p>Set Name: {{setName}}</p>
                    <p>EUR Price: {{this.prices.eur}}</p>
                    <p>Tix Price: {{this.prices.tix}}</p>
                    <p>USD Price: {{this.prices.usd}}</p>
                    <p>USD Foil Price: {{this.prices.usdFoil}}</p>
                    <!-- <p>Set Link: <a :href="setLink">Click Me! (Doesn't Work Yet)</a></p> -->
                    <hr>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
import axios from 'axios';

export default {
    data(){
        return{
            cardName: '',
            cardID: '',
            artistName: '',
            isBooster: '',
            collectorNumber: '',
            imageLink: '',
            releaseDate: '',
            setName: '',
            prices: {
                eur: '',
                tix: '',
                usd: '',
                usdFoil: ''
            },
            isLoaded: false
        }
    },
    props:{
        cardProfileSearchName: String,
        // cardProfileSearchTrigger: Function
    },
    filters:{
        toUpperCase(value){
            return value.toUpperCase();
        }
    },
    watch:{
        cardProfileSearchName: function(newVal, oldVal){
            axios.get(`https://api.scryfall.com/cards/named?exact=${newVal}`)
            .then( ({data}) => {

                this.isLoaded = true

                this.cardName = data.name
                this.cardID = data.id
                this.artistName = data.artist
                this.isBooster = data.booster
                this.collectorNumber = data.collector_number
                this.imageLink = data.image_uris.normal
                this.releaseDate = data.released_at
                this.setName = data.set_name
                //this.setLink = data.set_uri
                this.prices.eur = data.prices.eur
                this.prices.tix = data.prices.tix
                this.prices.usd = data.prices.usd
                this.prices.usdFoil = data.prices.usd_foil

            })
            .catch(error => console.log(error))
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
