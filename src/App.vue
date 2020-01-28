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