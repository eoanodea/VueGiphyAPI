<template>
    <b-dropdown id="dropdown-1" text="Gifs to display" class="m-md-2 float-right" variant="success" v-model="number">
        <b-dropdown-item v-for="option in options" v-bind:key="option" @click="updateNum(option)">{{option}}</b-dropdown-item>
    </b-dropdown>
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