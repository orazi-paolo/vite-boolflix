<script>
export default {
  data() {
    return {
        imgPath: 'https://image.tmdb.org/t/p/w342'
      
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
        }
    }
}
</script>

<template>
    <ul>
        <li><img :src="`${imgPath}${imgPoster}`" :alt="name"></li>
        <li>{{ name }}</li>
        <li> {{ originalName }}</li>
        <li><img class="language" :src="flag" :alt="language" @error="imgError"></li>
        <li>{{ vote }}</li>

    </ul>
</template>

<style lang="scss" scoped>
.language {
    height: 10px;
}

</style>