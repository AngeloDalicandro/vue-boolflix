<template>
    <div class="container">
        <ul>
            <li v-for="movie in movies" :key="movie.id">
                {{ movie.title }}
                {{ movie.original_title }}
                {{ movie.original_language }}
                {{ movie.vote_average }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "MainContainer",
    data() {
        return {
             
        }
    },
    props: {
        movies: Array
    },
    methods: {
        
    }
}
</script>

<style lang="scss" scoped>

</style>