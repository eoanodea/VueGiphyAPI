/*
 * File: App.vue
 * Project: vue-giph
 * File Created: Tuesday, 28th January 2020 1:18:31 pm
 * Author: Eoan O'Dea - eoan@wspace.ie
 * ---------------
 * File Description: Entry point for the application
 * Last Modified: Wednesday, 29th January 2020 3:20:30 pm
 * Modified By: Eoan O'Dea - eoan@wspace.ie
 * ---------------
 * Copyright 2020 - WebSpace
 */



<template>
  <b-container class="main-container">
    <b-row>
      <b-col>
        <list-giphs></list-giphs>
      </b-col> 
    </b-row>
  </b-container>
</template>

<script>
  import ListGiphs from '@/components/ListGiphs'

  export default {
    name: 'app',
    components: {
      ListGiphs
    }
}
</script>

<style scoped>
  .main-container {
    margin-top: 100px;
  }
</style>