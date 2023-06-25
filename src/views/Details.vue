<template>
    <div class="details-container">
        <!-- Link to go back to homepage -->
        <router-link :to="{name:'home'}">
            <div id="go-home">
                <img src="../components/icons/arrow.svg" id="arrow-icon"/>
                <p id="explore-back">Explore</p>
            </div>
        </router-link>
        
        <div class="book-details">
            <div class="book-rating">
                <!-- short version of book details component -->
                <Book :book="book"/>
                <!-- current star rating -->
                <CurrentRating :book="book"/>
            </div>
            <p class="book-description">{{ book.description }}</p>
        </div>
        <!-- the review form for the book -->
        <ReviewForm :book="book" :submitted="submitted" :errorIncurred="errorIncurred" @add-review="addReview"/>
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
                submitted: false,
                errorIncurred: false
            }
        },
        components: {
            Book,
            CurrentRating,
            ReviewForm
        },  
        methods: {
            // A function to get a book by id, takes in an ID
            async getBookById(bookId) {
                const res = await fetch(`http://localhost:5000/books/${bookId}`)

                const data = await res.json()
                
                return data;
            },
            // A function that sends a post request to an external API, takes in a review object
            async addReview(review) {
                try {
                    //in case we set the errorIncurred to true
                    this.errorIncurred=false
                    const res = await fetch('https://enr2djwmu4o1.x.pipedream.net', {
                        method: 'POST',
                        headers: {
                        'Content-type': 'application/json',
                        },
                        body: JSON.stringify(review),
                   })
                // set the submitted to true, to display the success message
                this.submitted = true; 
                } catch (error) {
                    this.errorIncurred=true
                    return
                }

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

    .book-details {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 24px;
        align-self: stretch;
    }

    .book-rating {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 24px;
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

    @media (min-width: 800px) {
        .book-details {
            flex-direction: row;
        }

        .book-rating {
            width: 30%;
        }
        .book-description {
            width: 70%;
        }
    }
</style>