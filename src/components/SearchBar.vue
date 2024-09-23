<script>
export default {
    data() {
        return {
            content: "",
        }
    },
    methods: {
        search() {
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
    <header class="p-3">
        <div class="container">
            <nav class="d-flex justify-content-between align-items-center">
                <div>
                    <a href="#" class="text-danger"><h1>BOOLFLIX</h1></a>
                </div>
                <div>
                    <input type="text" v-model="content" placeholder="Search" @keyup.enter="search()">
                    <button @click="search()">Search</button>
                </div>
            </nav>
        </div>
    </header>
</template>

<style lang="scss" scoped>
header{
    background-color: black;
    nav{
        a{
            text-decoration: none;
            color: white;
        }
    }
}
</style>