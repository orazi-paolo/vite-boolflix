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
        },
        // creo dinamicamente il background-image
        backgroundStyle() {
        return {
            backgroundImage: `url(${this.imgPath}${this.imgPoster})`,
            backgroundSize: '100% 100%', 
            backgroundRepeat: 'no-repeat'
        }
    }
    }
}
</script>

<template>
    <div v-if="imgPoster" class="col" :style="backgroundStyle">
        <ul class="d-none list-unstyled pt-4 ps-2 pe-2">
            <li>Titolo: {{ title }}</li>
            <li>Titolo originale: {{ originalTitle }}</li>
            <li>Lingua: <img class="language" :src="flag" :alt="language" @error="imgError"></li>
            <li>
                <div>Voto:</div>
                <span v-for="n in 5" :key="n">
                    <i v-if="n <= starRating" class="fas fa-star"></i>
                    <i v-else class="far fa-star"></i>
                </span>
            </li>
    
        </ul>
    </div>
</template>

<style lang="scss" scoped>
.language {
    height: 10px;
}
.col{
    height: calc(100vh - 150px);
    cursor: pointer;
    &:hover{
        border: 3px solid white;
        ul{
            display: block !important;

            li{
                color: white;
            }
        }
        background-image: none !important;
        background-color: black !important;
        transition: all 0.5s;
    }
}
</style>