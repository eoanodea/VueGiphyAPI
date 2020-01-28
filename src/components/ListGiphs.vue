<template>
    <span>
        <search v-on:search="searchGiphy"></search>
        <div v-if="search" class="search-results-container" fade>
            <h2 >Search results for {{ search }}</h2>
            <b-button variant="danger" @click="trending">Clear Search</b-button>
        </div>
        <hr />
        <div v-if="gifs">
            <number-drop-down v-on:filter="filterNumOfGifs"></number-drop-down>
            <div class="clearfix"></div>
            <b-card-group columns>
            <b-card 
                v-for="gif in gifs" 
                :key="gif.id"
                :title="gif.title"
                :img-alt="gif.title"
                :img-src="gif.images.fixed_width.url"    
            >
            <a :href="gif.url" target="_blank" color="secondary" class="float-right">View</a>
            </b-card>
        </b-card-group>
        </div>
        <p v-else>No Giphys</p>
    </span>
</template>
<script>
    import axios from 'axios'
    import Search from './Search'
    import NumberDropDown from './NumberDropDown'

    const GIPHY_URL = 'https://api.giphy.com/v1/gifs'
    const MIX_GIPHY_KEY = process.env.VUE_APP_GIPHY_KEY

    export default {
        name: "GiphViewer",
        components: {
            Search,
            NumberDropDown
        },
        data() {
            return {
                gifs: [],
                search: null
            }
        },
        mounted() {
            this.trending()
        },
        methods: {
            trending(limit) {
                axios.get(`${GIPHY_URL}/trending?api_key=${MIX_GIPHY_KEY}&limit=${limit ? limit : 25}`)
                .then(response => {
                    this.search = null
                    this.gifs = response.data.data
                })
                .catch(error => console.log(error))
            },
            searchGiphy(param, limit) {
                axios.get(`${GIPHY_URL}/search?api_key=${MIX_GIPHY_KEY}&q=${param}&limit=${limit ? limit : 25}`)
                .then(response => {
                    this.search = param
                    this.gifs = response.data.data
                })
                .catch(error => console.log(error))
            },
            filterNumOfGifs(param) {
                this.search
                ? this.searchGiphy(this.search, param)
                : this.trending(param)
            }
        }
    }
</script>
<style scoped>
    .search-results-container {
        display: flex;
        justify-content: space-between
    }
</style>