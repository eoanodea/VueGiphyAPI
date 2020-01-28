<template>
  <b-container>
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
