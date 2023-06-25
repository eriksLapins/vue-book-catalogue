<template>
    <div class="details-container">
        <Book :book="book"/>
        <BookReview :book="book"/>

    </div>
</template>

<script>
    import Book from '../components/Book.vue'
    import BookReview from '../components/BookReview.vue'
    export default {
        name: "Details",
        data() {
            return {
                id: '',
                book: {}
            }
        },
        components: {
            Book,
            BookReview
        },  
        methods: {
            async getBookById(bookId) {
                const res = await fetch(`http://localhost:5000/books/${bookId}`)

                const data = await res.json()
                
                return data;
            },
        },
        async created() {
            this.id = this.$route.params.bookId;
            this.book = await this.getBookById(this.id);
        }
    }
</script>

<style scoped>
    .details-container {
        display: flex;
        width: 100%;
        padding: 0px 16px;
        flex-direction: column;
        align-items: flex-start;
        gap: 32px;
    }

</style>