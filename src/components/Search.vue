<template>
    <input 
        name="search"
        placeholder="Search for a book"
        type="text"
        v-model="searchTerm"
    />    
</template>

<script>
    export default {
        name: 'Search',
        data() {
            return {
                searchTerm: ''
            }
        },
        watch: {
                searchTerm(newSearchTerm) {
                    this.$emit('change-value', newSearchTerm);
                }
        }
    }
</script>