/*
 * File: NumberDropDown.vue
 * Project: vue-giph
 * File Created: Tuesday, 28th January 2020 3:46:37 pm
 * Author: Eoan O'Dea - eoan@wspace.ie
 * ---------------
 * File Description: Filters the amount of Giphs to be displayed, 
 * returns the number to ListGiphs.vue
 * Last Modified: Wednesday, 29th January 2020 3:20:17 pm
 * Modified By: Eoan O'Dea - eoan@wspace.ie
 * ---------------
 * Copyright 2020 - WebSpace
 */



<template>
    <b-nav-item-dropdown id="dropdown-1" text="Gifs to display" class="m-md-2" v-model="number" right>
        <b-dropdown-item v-for="option in options" v-bind:key="option" @click="updateNum(option)">{{option}}</b-dropdown-item>
    </b-nav-item-dropdown> 
</template>

<script>
    export default {
        name: 'NumberDropDown',
        data() {
            return {
                number: 10,
                options: [5, 10, 30, 60]
            }
        },
        methods: {
            updateNum(num) {
                this.number = num
                this.$emit('filter', this.number)
            }
        }
    }
</script>