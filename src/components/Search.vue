<template>
    <b-form inline class="search-form-containr">
        <div class="search-form-inputs">
            <b-input type="text" v-model="term" v-on:keydown.enter="searchGiphy($event)"/>
            <b-button variant="primary" @click="searchGiphy($event)">Search</b-button>
        </div>
        <b-form-invalid-feedback class="search-error" :state='!hasError'>{{error}}</b-form-invalid-feedback>
    </b-form>
</template>

<script>

  export default {
    name: 'Search',
    data() {
        return {
            term: '',
            error: null,
            hasError: false
        }
    },
    components: {
      //
    },
    methods: {
        searchGiphy(e) {
            e.preventDefault()
            if(!this.term) {
                this.error = "Please enter a valid search"
                this.hasError = true
            }
            else {
                this.hasError = false
                this.error = null
                this.$emit('search', this.term)
                this.term = ""
            }
        }
    }
}
</script>
<style scoped>
    .search-form-containr {
        display: flex;
        position: relative;
    }
    .search-form-inputs {
        display: flex;
        flex-direction: row;
    }
    .search-form-inputs input, .search-form-inputs button {
        border-radius: 0
    }
    .search-error {
        position: absolute;
        bottom: -15px;
        left: 0;
    }
</style>
