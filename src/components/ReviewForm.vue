<template>
    <form @submit="onSubmit" class="review-form" v-if="!submitted">
        <h2>Write a review <p class="error-text" v-if="errorIncurred">Something went wrong, please try again later</p></h2>
        <h3>Rate the book</h3>
        <div class="star-rating">
            <star-rating
            :increment="1"
            :rounded-corners="true"
            :border-color="['#FFC163'][0]"
            :border-width="4"
            inactive-color="#fff"
            active-color="#FFC163"
            :star-size="24"
            :show-rating="false"
            v-model:rating="rating"
            ></star-rating>
            <p class="stars-error" v-if="tooLittleStars">Please rate the book with at least 1 star</p>
        </div>
        <textarea type="text" v-model="reviewText" class="review-text"></textarea>
        <div class="submit-button">
            <button type="submit">Submit Review</button>
        </div>
    </form>
    <div class="thank-you-container" v-if="submitted">
        <p>Thank you! Review recieved.</p>
    </div>
</template>

<script scoped>
    import {uuid} from 'vue-uuid'
    import StarRating from 'vue-star-rating'
    
    export default {
        name: "ReviewForm",
        data() {
            return {
                rating: 0,
                reviewText: '',
                tooLittleStars: false
            }
        },
        props: {
            book: Object,
            submitted: Boolean,
            errorIncurred: Boolean
        },
        components: {
            StarRating
        },
        emits: ['add-review'],
        methods: {
            onSubmit(e) {
                e.preventDefault()

                if (this.rating==0) {
                    this.tooLittleStars=true
                    return
                }
                
                // create a new review Object
                const newReview = {
                    id: uuid.v4(),
                    reviewText: this.reviewText,
                    rating: this.rating,
                    bookId: this.book.id
                }

                // emit an add review event and send the review object
                this.$emit('add-review', newReview)
                this.rating = 0
                this.reviewText = ''
                // in case we just had an error with stars, we set the error boolean back to false
                this.tooLittleStars=false
                },
        }
    }
</script>

<style scoped>

    .review-form {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        gap: 24px;
        align-self: stretch;
    }
    .review-text {
        height: 208px;
        align-self: stretch;
        border-radius: 4px;
        border: 1px solid var(--ui-grey, #DDE1E3);
        background: #FFF;
    }

    h2, h3 {
        align-self: stretch;
        color: var(--typography-dark, rgba(0, 0, 0, 0.95));
        font-weight: 700;
    }

    h2 {
        font-size: 24px;
        display: flex;
        flex-direction: row;
        align-items: center;
        gap: 32px;
    }

    h3 {
        font-size: 18px;
    }

    .submit-button {
        display: flex;
        padding: 10px;
        justify-content: center;
        align-items: center;
        gap: 10px;
        align-self: stretch;
        border-radius: 24px;
        border: 2px solid var(--ui-primary, #3980B2);
    }

    button {
        color: var(--ui-primary, #3980B2);
        background-color: #fff;
        border: none;
        /* Body Bold */
        font-size: 16px;
        font-weight: 700;
        line-height: 24px;
    }
    .thank-you-container {
        display: flex;
        padding: 10px;
        align-items: flex-start;
        gap: 10px;
        border-radius: 4px;
        background: var(--ui-light-blue, #CFEBFF);
    }

    .thank-you-container p {
        color: var(--typography-dark, rgba(0, 0, 0, 0.95));
        font-size: 14px;
        font-weight: 700;
    }


    .error-text {
        color: red;
        font-weight: bold;
        font-size: 20px;
    }
    .stars-error {
        color: red;
        font-weight: bold;
        font-size: 16px;
    }

    .star-rating {
        display: flex;
        flex-direction: row;
        gap: 32px;
    }

</style>