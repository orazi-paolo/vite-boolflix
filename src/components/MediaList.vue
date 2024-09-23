<script>
import MovieListCard from './MovieListCard.vue';
import SerieTvListCard from './SerieTvListCard.vue';
export default {
    data() {
        return {

        }
    },
    components: {
        MovieListCard,
        SerieTvListCard
    },
    props: {
        movieList: {
            type: Array,
            required: true
        },
        serieTvList: {
            type: Array,
            required: true
        }
    }
}
</script>

<template>

    <MovieListCard v-for="movie in movieList" :key="movie.id" :title="movie.title"
        :original-title="movie.original_title" :language="movie.original_language" :vote="movie.vote_average"/>
    <SerieTvListCard v-for="tv in serieTvList" :key="tv.id" 
    :name="tv.name" :original-name="tv.original_name" :language="tv.original_language" :vote="tv.vote_average" />

</template>

<style scoped></style>