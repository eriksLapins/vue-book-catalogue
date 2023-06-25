<template>
    <div class="book-list-item">
        <div class="image-container" :style="{ backgroundImage: 'url(' + book.image + ')' }">
        </div>
        <div class="description-short">
            <h2 class="title">{{ book.title }}</h2>
            <p class="author medium-typography">{{ book.author }}</p>
            <p class="price typography-dark">{{ book.price }}</p>
            <p class="publisher medium-typography">{{ book.publisher }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Book',
        props: {
            book: Object,
        }
    }
</script>

<style scoped>
    .book-list-item {
        display: flex;
        align-items: flex-start;
        gap: 14px;
        align-self: stretch;
    }

    .image-container {
        width: 88px;
        height: 110px;
        background-size: cover;
    }

    .title {
        align-self: stretch;
        color: var(--typography-dark, rgba(0, 0, 0, 0.95));
        /* Body Bold */
        font-size: 16px;
        font-weight: 700;
        line-height: 24px;
    }

    .medium-typography {
        color: var(--typography-medium, rgba(0, 0, 0, 0.70));
        /* Caption Regular */
        font-size: 14px;
    }

    .typography-dark {
        color: var(--typography-dark, rgba(0, 0, 0, 0.95));
        /* Caption Bold */
        font-size: 14px;
        font-weight: 700;
    }


</style>

