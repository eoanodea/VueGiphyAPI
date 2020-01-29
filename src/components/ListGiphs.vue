/*
 * File: ListGiphs.vue
 * Project: vue-giph
 * File Created: Tuesday, 28th January 2020 1:45:36 pm
 * Author: Eoan O'Dea - eoan@wspace.ie
 * ---------------
 * File Description: Includes the App Navigation bar, 
 * and list of Giphs which can either be trending or a search result
 * Last Modified: Wednesday, 29th January 2020 3:19:00 pm
 * Modified By: Eoan O'Dea - eoan@wspace.ie
 * ---------------
 * Copyright 2020 - WebSpace
 */



<template>
    <span>
        <b-navbar type="dark" variant="dark" class="nav" toggleable="md">
            <b-navbar-brand>
                Vue.js Giphy API
            </b-navbar-brand>

            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>
            
            
            <b-navbar-nav class="ml-auto">
                <search v-on:search="searchGiphy"></search>
                <number-drop-down v-on:filter="filterNumOfGifs"></number-drop-down>
            </b-navbar-nav>

            </b-collapse>
        </b-navbar>
        
        <div v-if="search" class="search-results-container" fade>
            <h2 >Search results for {{ search }}</h2>
            <b-button variant="danger" @click="trending">Clear Search</b-button>
        </div>
        <h2 v-else>Trending </h2>
        <hr />
        <div v-if="gifs">
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
        <p v-else>No Giphys Found</p>
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
    .nav {
        position: fixed;
        top: 0;
        left: 0;
        z-index: 1;
        width: 100%;
    }
</style>