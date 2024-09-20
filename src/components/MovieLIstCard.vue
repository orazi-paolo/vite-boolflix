<script>
export default {
    data() {
        return {

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
        <li>{{ title }}</li>
        <li> {{ originalTitle }}</li>
        <li><img :src="flag" :alt="language" @error="imgError"></li>
        <li>{{ vote }}</li>

    </ul>
</template>

<style lang="scss" scoped>
img {
    height: 10px;
}
</style>