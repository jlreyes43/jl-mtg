<template>
    <div class="text-white text-left">
        <p>{{ cardProfileSearchName }}</p>
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
        <!-- <p>Set Link: <a :href="setLink">Click Me! (Doesn't Work Yet)</a></p> -->
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
            }
        }
    },
    props:{
        cardProfileSearchName: String,
        // cardProfileSearchTrigger: Function
    },
    watch:{
        cardProfileSearchName: function(newVal, oldVal){
            axios.get(`https://api.scryfall.com/cards/named?exact=${newVal}`)
            .then( ({data}) => {
                console.log(data)
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
