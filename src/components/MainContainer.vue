<template>
    <div class="container">
        <ul>
            <li v-for="movie in movies" :key="movie.id">
                {{ movie.title }}
                {{ movie.original_title }}
                <img :src="languageImgUrl + enIsNotANation(movie.original_language)" :alt="`Original language: ${language[movie.original_language]}`">
                {{ movie.vote_average }}
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
        movies: Array
    },
    methods: {
        enIsNotANation(x) {
            if( x === "en") {
                return "gb"
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