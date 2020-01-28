<template>
    <span>
        <search v-on:search="searchGiphy"></search>
        <b-card-group columns v-if="gifs">
            <b-card 
                v-for="gif in gifs" 
                :key="gif.id"
                :title="gif.title"
                :img-alt="gif.title"
                :img-src="gif.images.fixed_width.url"    
            >

            </b-card>
        </b-card-group>
        <p v-else>No Giphys</p>
    </span>
</template>
<script>
    import axios from 'axios'
    import Search from './Search'

    const GIPHY_URL = 'https://api.giphy.com/v1/gifs'
    const MIX_GIPHY_KEY = process.env.VUE_APP_GIPHY_KEY

    export default {
        name: "GiphViewer",
        components: {
            Search
        },
        data() {
            return {
                gifs: []
            }
        },
        mounted() {
            axios.get(`${GIPHY_URL}/trending?api_key=${MIX_GIPHY_KEY}`)
                .then(response => {
                    
                    this.gifs = response.data.data
                })
                .catch(error => console.log(error))
        },
        methods: {
            searchGiphy(param) {
                axios.get(`${GIPHY_URL}/search?api_key=${MIX_GIPHY_KEY}&q=${param}`)
                .then(response => {
                    this.gifs = response.data.data
                })
                .catch(error => console.log(error))
            }
        }
    }
</script>