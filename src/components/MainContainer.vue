<template>
    <div class="container">

        <h2>Film</h2>

        <ul>
            <MovieCard v-for="movie in movies" :key="movie.id"
            :movie="movie"
            />
        </ul>
        
        <h2>Serie TV</h2>

        <ul>
            <SeriesCard v-for="series in tvSeries" :key="series.id"
            :series="series"
            />
        </ul>

        <ul>

        </ul>
    </div>    

</template>

<script>
import MovieCard from "./MovieCard.vue";
import SeriesCard from "./SeriesCard.vue";

export default {
    name: "MainContainer",
    components: {
        MovieCard,
        SeriesCard
    },
    props: {
        movies: Array,
        tvSeries: Array
    }
}
</script>

<style lang="scss" scoped>
.container {
    
    h2 {
        margin: 1rem;
        font-size: 3rem;
        color: white;
    }

    ul {
        list-style-type: none;
        display: flex;
        flex-wrap: wrap;
    }
}



</style>