<template>
    <div class="container">
        <ul>
            <li v-for="movie in movies" :key="movie.id">
                {{ movie.title }}
                {{ movie.original_title }}
                <img :src="languageImgUrl + enIsNotANation(movie.original_language)" :alt="`Original language: ${language[movie.original_language]}`">
                {{ movie.vote_average }}
            </li>

            <li v-for="series in tvSeries" :key="series.id">
                {{ series.name }}
                {{ series.original_name }}
                <img :src="languageImgUrl + enIsNotANation(series.origin_country[0])" :alt="`Original language: ${language[series.original_language]}`">
                {{ series.vote_average }}
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
            language: languagesList,
            languageImgUrl: "https://countryflagsapi.com/svg/",
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
        }
    }
}
</script>

<style lang="scss" scoped>
    img {
        width: 1rem;
    }
</style>