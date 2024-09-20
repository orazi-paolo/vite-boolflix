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
    }
}
</script>

<template>
    <ul>
        <li>{{ title }}</li>
        <li> {{ originalTitle }}</li>
        <li>{{ language }}</li>
        <li>{{ vote }}</li>

    </ul>
</template>

<style scoped></style>