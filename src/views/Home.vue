<template>
    <h1>Hello World</h1>
    <Results />
</template>

<script scoped>
    import Results from '../components/Results.vue'

    export default {
        name: 'Home',
        components: {
            Results,
        }
    }
</script>