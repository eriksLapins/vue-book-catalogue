<template>
    <div class="current-rating-container">
        <p class="book-rating typography-light">{{ book.rating }}</p>
        <!-- current star rating of the book -->
        <star-rating 
            class="current-rating"
             :increment="0.1"
             :rounded-corners="true"
             :border-color="['#FFC163'][0]"
             :border-width="4"
             inactive-color="#fff"
             active-color="#FFC163"
             :star-size="24"
             :rating="book.rating"
             :show-rating="false"
             :read-only="true">
        </star-rating>
    </div>

</template>

<script>
import StarRating from 'vue-star-rating'
export default {
    name: "CurrentRating",
    props: {
        book: Object,
    },
    components: {
        StarRating
    }
}
</script>

<style scoped>
    .current-rating-container {
        display: flex;
        flex-direction: row;
        align-items: flex-start;
        gap: 4px;
        align-self: stretch;
    }
    .typography-light {
        color: var(--typography-light, rgba(0, 0, 0, 0.55));
        font-size: 16px;
        line-height: 24px;
    }

    .current-rating > svg > polygon {
        border: 1px solid #FFC163;
    }

</style>