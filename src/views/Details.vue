<template>
    <div class="details-container">
        <div id="go-home">
            <img src="../components/icons/arrow.svg" id="arrow-icon"/><router-link :to="{name:'home'}" id="explore-back">Explore</router-link>
        </div>
        <Book :book="book"/>
        <CurrentRating :book="book"/>
        <p class="book-description">{{ book.description }}</p>
        <ReviewForm :book="book" @add-review="addReview"/>
    </div>
</template>

<script>
    import Book from '../components/Book.vue'
    import CurrentRating from '../components/CurrentRating.vue'
    import ReviewForm from '../components/ReviewForm.vue'
    export default {
        name: "Details",
        data() {
            return {
                id: '',
                book: {},
            }
        },
        components: {
            Book,
            CurrentRating,
            ReviewForm
        },  
        methods: {
            async getBookById(bookId) {
                const res = await fetch(`http://localhost:5000/books/${bookId}`)

                const data = await res.json()
                
                return data;
            },
            async addReview(review) {
                const res = await fetch('https://enr2djwmu4o1.x.pipedream.net', {
                    method: 'POST',
                    headers: {
                    'Content-type': 'application/json',
                    },
                    body: JSON.stringify(review),
                })
            }
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

    #go-home {
        display: flex;
        align-items: flex-start;
        gap: 4px;
        align-self: stretch;
    }

    #explore-back {
        color: var(--typography-dark, rgba(0, 0, 0, 0.95));
        font-size: 16px;
        font-weight: 700;
        line-height: 24px;
        text-decoration-line: underline;
    }


</style>