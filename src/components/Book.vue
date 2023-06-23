<template>
    <div class="book-list-item">
        <img :src="book.image" style="width:50px"/>
        <div class="description-short">
            <h2>{{ book.title }}</h2>
            <p class="author">{{ book.author }}</p>
            <p class="price">{{ book.price }}</p>
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
</style>

