<script>
import axios from 'axios';
export default {
  data() {
    return {
        imgPath: 'https://image.tmdb.org/t/p/w342',
        apikey: '326b39b723b5e214fc6441c1e27fb3ed',
        apiUrlActors: 'https://api.themoviedb.org/3/movie/',
        actors: []

    }
  },
  props: {
    name: {
      type: String,
      required: true
    },
    originalName: {
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
      required: false,
    },
    id:{
      type: Number,
      required: true
    }
  },
    methods: {
      // faccio la chiamata all'API per avere indietro gli attori
      getApiActors() {
        axios.get(`${this.apiUrlActors}${this.id}/credits`, {
            params: {
                // l unico parametro di cui ho bisogno è la mia chiave
            api_key: this.apikey,
        }
        })
        .then((response) => {
          console.log(response);
          this.actors = response.data.cast.slice(0, 5);
        })
        .catch(function (error) {
          console.log(error);
        })
        .finally(function () {
          console.log('chiamata attori terminata')
        });
    },
        imgError(event) {
            event.target.src = '/default.jpg';
        },
        
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
    },
    mounted() {
        this.getApiActors();
    }
}
</script>

<template>
  <div v-if="imgPoster" class="col" :style="backgroundStyle">
    <ul class="d-none list-unstyled pt-4 ps-2 pe-2">
        <li>Titolo: {{ name }}</li>
        <li>Titolo originale: {{ originalName }}</li>
        <li>Lingua: <img class="language" :src="flag" :alt="language" @error="imgError"></li>
        <li>
          <div>Voto:</div>
          <span v-for="n in 5" :key="n">
                <i v-if="n <= starRating" class="fas fa-star"></i>
                <i v-else class="far fa-star"></i>
            </span>
        </li>
        <li v-if="actors.length > 0">
            <div>Attori principali:</div>
            <ul>
              <li v-for="actor in actors" :key="actor.id">
                {{ actor.name }}
             </li>
            </ul>
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