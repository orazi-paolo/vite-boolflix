<script>
import SearchBar from './components/SearchBar.vue';
import MediaList from './components/MediaList.vue';
import axios from 'axios';

export default {
  data() {
    return {
      apiUrlMovie: 'https://api.themoviedb.org/3/search/movie?',
      apiUrlTv: 'https://api.themoviedb.org/3/search/tv',
      apikey: '326b39b723b5e214fc6441c1e27fb3ed',
      movieList: [],
      serieTvList: [],
    }
  },
  components: {
    SearchBar,
    MediaList
  },
  methods: {
    // faccio la chiamata all'API
    getApiMovie(content) {
      axios.get(this.apiUrlMovie, {
        params: {
          // metto come parametri la mia chiave e il contenuto della ricerca
          api_key: this.apikey,
          query: content,
        }
      })
        .then((response) => {
          // controllo che query mi sta arrivando
          console.log(content);
          // controllo la risposta che in questo caso mi restituisce un array di oggetti
          console.log(response.data.results);
          // assegno alla variabile movieList l'array di oggetti
          this.movieList = response.data.results;
        })
        .catch(function (error) {
          console.log(error);
        })
        .finally(function () {
          console.log('chiamata film terminata')
        });
    },
    getApiTv(content) {
      axios.get(this.apiUrlTv, {
        params: {
          // metto come parametri la mia chiave e il contenuto della ricerca
          api_key: this.apikey,
          query: content,
        }
      })
        .then((response) => {
          // controllo la risposta che in questo caso mi restituisce un array di oggetti
          console.log(response.data.results);
          // assegno alla variabile serieTvList l'array di oggetti
          this.serieTvList = response.data.results;
        })
        .catch(function (error) {
          console.log(error);
        })
        .finally(function () {
          console.log('chiamata serie tv terminata')
        });
    }
  }
}
</script>

<template>

  <SearchBar @search-movie="getApiMovie" @search-tv="getApiTv" />
  <MediaList :movieList="movieList" :serieTvList="serieTvList" />

</template>

<style lang="scss">
@use 'bootstrap/scss/bootstrap.scss';
body {
  background-color: grey;
}
</style>
