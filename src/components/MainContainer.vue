<template>
    <div class="container">

        <div v-if="movies.length">
            <h2>Film</h2>

            <ul>
                <MovieCard v-for="singleMovie in filteredMoviesByGenre" :key="singleMovie.id"
                :movie="singleMovie"
                />
            </ul>

        </div>
        
        <div v-if="tvSeries.length">
            <h2>Serie TV</h2>

            <ul>
                <SeriesCard v-for="singleSeries in filteredSeriesByGenre" :key="singleSeries.id"
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
        tvSeries: Array,
        userSelectedGenre: Number
    },
    computed: {
        filteredMoviesByGenre() {
            let filterArray = []; 
            if(this.userSelectedGenre === 420) {
                return this.movies;
            } else {
                this.movies.forEach((movie) => {
                    movie.genre_ids.forEach((genre) => {
                        if(this.userSelectedGenre === genre) {
                            filterArray.push(movie);
                        }
                    })
                })
                return filterArray;
            }
            
        },
        filteredSeriesByGenre() {
            let filterArray = []; 
            if(this.userSelectedGenre === 420) {
                filterArray = this.tvSeries;
            } else {
                this.tvSeries.forEach((series) => {
                    series.genre_ids.forEach((genre) => {
                        if(this.userSelectedGenre === genre) {
                            filterArray.push(series);
                        }
                    })
                })
            }
            return filterArray
        }
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
        justify-content: space-evenly;
        flex-wrap: wrap;
    }
}



</style>