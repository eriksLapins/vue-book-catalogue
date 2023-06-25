<template>
    <div class="search-bar">
        <img src="./icons/search.svg" id="search-icon"/>
        <input 
            name="search"
            placeholder="Search for a book"
            type="text"
            v-model="searchTerm"
            class="search"
        />
    </div>
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

<style scoped>

    #search-icon {
        height: 24px;
        width: 24px;
    }

    .search {
        color: var(--typography-light, rgba(0, 0, 0, 0.55));
        border: none;
        font-size: 16px;
        line-height: 24px;
    }

    .search-bar {
        display: flex;
        padding: 8px;
        align-items: flex-start;
        gap: 10px;
        align-self: stretch;
        border-radius: 4px;
        border: 1px solid var(--ui-grey, #DDE1E3);
        background: #FFF;
    }
</style>