<template>
    <form @submit="onSubmit" class="review-form">
        <h2>Write a review</h2>
        <h3>Rate the book</h3>
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
        <textarea type="text" name="review-text" v-model="reviewText" class="review-text"></textarea>
        <button type="submit">Submit Review</button>
    </form>
</template>

<script scoped>
    import {uuid} from 'vue-uuid'
    import StarRating from 'vue-star-rating'
    export default {
        name: "ReviewForm",
        data() {
            return {
                rating: 0,
                reviewText: ''
            }
        },
        props: {
            book: Object,
        },
        components: {
            StarRating
        },
        methods: {
            onSubmit(e) {
                e.preventDefault()

                if (!this.reviewText) {
                    alert('Please add a task')
                    return
                }

                const newReview = {
                    id: uuid.v4(),
                    reviewText: this.reviewText,
                    rating: this.rating
                }
                
                this.$emit('add-review', newReview)
                this.rating = 0
                this.reviewText = ''
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

</style>