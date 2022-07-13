<template>
    <li>

        <img class="poster" v-if="didLoad === true" :src="productImgUrl + series.poster_path" @error="pictureLoadingError" :alt="series.name">
        <img class="poster" v-else :src="productImgUrl + series.backdrop_path"  :alt="series.name">

        <div class="product-info">
            <div class="title"> <b>Titolo: </b> {{ series.name }} </div>
            <div class="original-title"> {{ series.original_name }} </div>
            <div class="language">
                <b>Lingua:</b>
                <img :src="languageImgUrl + enIsNotANation(series.origin_country[0])" :alt="`Original language: ${language[series.original_language]}`">
            </div>
            <div class="votes">
                <b>Voto:</b>
                <span v-for="star, index in fromTenToFive(series.vote_average)" :key="index"><font-awesome-icon icon="fa-solid fa-star"/></span>
                <span v-for="emptyStar, index in ( maxVote - fromTenToFive(series.vote_average))" :key="index"><font-awesome-icon icon="fa-regular fa-star"/></span> 
            </div>
            <div class="overview"> <b>Trama:</b> {{ series.overview }} </div>
        </div>

    </li>
</template>

<script>
import languagesList from "../assets/languages.json";

export default {
    name: "SeriesCard",
    data() {
        return {
            maxVote: 5,
            language: languagesList,
            languageImgUrl: "https://countryflagsapi.com/svg/",
            productImgUrl: "https://image.tmdb.org/t/p/w342",
            didLoad: true
        }
    },
    props: {
        series: Object
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
        },
        pictureLoadingError() {
            this.didLoad = false;
        }
    }
}
</script>

<style lang="scss" scoped>
    @import "../styles/cards-style";
</style>