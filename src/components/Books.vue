<template>
    <div v-for="book in books" :key="book.id" class="book-list">
        <Book :book="book"/>
    </div>
</template>

<script>
    import Book from './Book.vue'

    export default {
        name: 'Books',
        props: {
            books: Array,
        },
        components: {
            Book,
        },
        
    }
</script>

<style scoped>
    .book-list {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 16px;
        align-self: stretch;
        }
</style>