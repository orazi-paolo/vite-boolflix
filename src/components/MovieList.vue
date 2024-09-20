<script>
import MovieListCard from './MovieListCard.vue';
export default {
    data() {
        return {

        }
    },
    components: {
        MovieListCard
    },
    props: {
        movieList: {
            type: Array,
            required: true
        }
    }
}
</script>

<template>

    <MovieListCard v-for="movie in movieList" :key="movie.id" :title="movie.title"
        :original-title="movie.original_title" :language="movie.original_language" :vote="movie.vote_average" />

</template>

<style scoped></style>