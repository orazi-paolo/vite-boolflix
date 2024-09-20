<script>
import SearchBar from './components/SearchBar.vue';
import MovieList from './components/MovieList.vue';
import axios from 'axios';

export default {
  data() {
    return {
      apiUrl: 'https://api.themoviedb.org/3/search/movie?',
      apikey: '326b39b723b5e214fc6441c1e27fb3ed',
      movieList: [],
    }
  },
  components: {
    SearchBar,
    MovieList
  },
  methods: {
    // faccio la chiamata all'API
    getApi(content) {
      axios.get(this.apiUrl, {
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
          console.log('chiamata terminata')
        });
    }
  }
}
</script>

<template>

  <SearchBar @search="getApi" />
  <MovieList :movieList="movieList" />

</template>

<style lang="scss"></style>
