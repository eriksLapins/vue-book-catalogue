<template>
    <div class="book-list">
        <router-link :to="{ name: 'details', params: { bookId: book.id }}" v-for="book in books" :key="book.id">
                <Book :book="book"/>
        </router-link>
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
        }        
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
    @media (min-width: 800px) {
        .book-list {
            display: grid;
            grid-template-columns: auto auto auto;
            gap: 37px 24px;
        }
    }

    @media (min-width: 1200px) {
        .book-list {
            gap: 32px 24px;
        }
    }
</style>