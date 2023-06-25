<template>
    <div class="home-container">
        <Search @change-value="filterSearch"/>
        <Books :books="books"/>
    </div>
</template>

<script scoped>
    import Books from '../components/Books.vue'
    import Search from '../components/Search.vue'
    export default {
        name: 'Home',
        components: {
            Books,
            Search
        },
        data() {
            return {
                initialBooks: [],
                books: [],
            }
        },
        methods: {
            // function get the list of all books
            async getBooks() {
                const res = await fetch('http://localhost:5000/books')

                const data = await res.json()
                
                return data;
            },

            // filter out the searched for books
            async filterSearch(searchTerm) {
                // each time we check the initial books list
                const bookList = this.initialBooks
                const filteredList = bookList.filter((book) => {
                    return book.title.toLowerCase().includes(searchTerm.toLowerCase())
                })

                this.books = filteredList;
            }
        },

        // function that sets books list to the retrieved books
        async created() {
            this.books = await this.getBooks();
            // copy the books array (displayed on page)
                // this is for limiting the requests to external endpoint
            this.initialBooks = this.books;
        },
    }
</script>

<style scoped>
    .home-container {
        display: flex;
        width: 100%;
        padding: 0px 16px;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 32px;
    }
</style>