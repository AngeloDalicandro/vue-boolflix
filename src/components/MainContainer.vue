<template>
    <div class="container">
        <ul>
            <li v-for="movie in movies" :key="movie.id">
                <img class="poster" :src="productImgUrl + movie.poster_path" :alt="movie.title">
                {{ movie.title }}
                {{ movie.original_title }}
                <img :src="languageImgUrl + enIsNotANation(movie.original_language)" :alt="`Original language: ${language[movie.original_language]}`">
                <span v-for="star, index in fromTenToFive(movie.vote_average)" :key="index"><font-awesome-icon icon="fa-solid fa-star"/></span>
                <span v-for="emptyStar, index in ( maxVote - fromTenToFive(movie.vote_average))" :key="index"><font-awesome-icon icon="fa-regular fa-star"/></span> 
            </li>

            <li v-for="series in tvSeries" :key="series.id">
                <img class="poster" :src="productImgUrl + series.poster_path" :alt="series.name">
                {{ series.name }}
                {{ series.original_name }}
                <img :src="languageImgUrl + enIsNotANation(series.origin_country[0])" :alt="`Original language: ${language[series.original_language]}`">
                <span v-for="star, index in fromTenToFive(series.vote_average)" :key="index"><font-awesome-icon icon="fa-solid fa-star"/></span>
                <span v-for="emptyStar, index in ( maxVote - fromTenToFive(series.vote_average))" :key="index"><font-awesome-icon icon="fa-regular fa-star"/></span> 
            </li>
        </ul>
    </div>
</template>

<script>
import languagesList from "../assets/languages.json";

export default {
    name: "MainContainer",
    data() {
        return {
            maxVote: 5,
            language: languagesList,
            languageImgUrl: "https://countryflagsapi.com/svg/",
            productImgUrl: "https://image.tmdb.org/t/p/w342"
        }
    },
    props: {
        movies: Array,
        tvSeries: Array
    },
    methods: {
        enIsNotANation(x) {
            if( x === "en") {
                return "gb"
            } else if( x === "ko") {
                return "kr"
            } else {
                return x
            }
        },
        fromTenToFive(number) {
            return Math.round(number / 2)
        }
    }
}
</script>

<style lang="scss" scoped>
    img {
        width: 1rem;

        &.poster {
            width: 342px;
        }
    }


</style>