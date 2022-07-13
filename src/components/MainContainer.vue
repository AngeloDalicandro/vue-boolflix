<template>
    <div class="container">

        <div v-if="movies.length">
            <h2>Film</h2>

            <ul>
                <MovieCard v-for="singleMovie in movies" :key="singleMovie.id"
                :movie="singleMovie"
                />
            </ul>

        </div>
        
        <div v-if="tvSeries.length">
            <h2>Serie TV</h2>

            <ul>
                <SeriesCard v-for="singleSeries in tvSeries" :key="singleSeries.id"
                :series="singleSeries"
                />
            </ul>

        </div>

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
    },
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
        justify-content: space-evenly;
        flex-wrap: wrap;
    }
}



</style>