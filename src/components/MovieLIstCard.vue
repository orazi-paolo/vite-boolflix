<script>
export default {
    data() {
        return {
            imgPath: 'https://image.tmdb.org/t/p/w342'

        }
    },
    props: {
        title: {
            type: String,
            required: true
        },
        originalTitle: {
            type: String,
            required: true
        },
        language: {
            type: String,
            required: true
        },
        vote: {
            type: Number,
            required: true
        },
        imgPoster: {
            type: String,
            required: false
        }
    },
    methods: {
        imgError(event) {
            event.target.src = '/default.jpg';
        }
    },
    computed: {
        // creo una computed property per gestire le bandiere
        flag() {
            if (this.language === 'en') {
                return `/gb.png`;
            }
            return `/${this.language}.png`;
        },
        // creo una computed che mi trasforma il voto in una scala da 1 a 5 per le stelle
        starRating() {
            console.log(Math.ceil(this.vote));
            return Math.ceil((Math.ceil(this.vote) / 10) * 5);
        }
    }
}
</script>

<template>
    <ul>
        <li><img :src="`${imgPath}${imgPoster}`" :alt="title"></li>
        <li>{{ title }}</li>
        <li> {{ originalTitle }}</li>
        <li><img class="language" :src="flag" :alt="language" @error="imgError"></li>
        <li>
            <span v-for="n in 5" :key="n">
                <i v-if="n <= starRating" class="fas fa-star"></i>
                <i v-else class="far fa-star"></i>
            </span>
        </li>

    </ul>
</template>

<style lang="scss" scoped>
.language {
    height: 10px;
}
</style>