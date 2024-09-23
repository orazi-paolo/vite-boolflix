<script>
export default {
    data() {
        return {
            content: "",
        }
    },
    methods: {
        search() {
            // stampo in console per controllare se prendo il valore corretto
            console.log(this.content);
            // invio il valore al padre per i film
            this.$emit("searchMovie", this.content);
            // invio il valore al padre per le serie tv
            this.$emit("searchTv", this.content);
            // lo resetto dopo aver fatto la ricerca
            this.content = "";
        }
    }
}
</script>

<template>
    <header>
        <nav>
            <input type="text" v-model="content">
            <button @click="search()">Search</button>
        </nav>
    </header>
</template>

<style scoped></style>