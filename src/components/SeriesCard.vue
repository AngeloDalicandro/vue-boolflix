<template>
    <li>

        <img class="poster" :src="productImgUrl + series.poster_path" :alt="series.name">

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
            productImgUrl: "https://image.tmdb.org/t/p/w342"
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
        }
    }
}
</script>

<style lang="scss" scoped>
    li {
        margin: 1rem;
        position: relative;
        width: 342px;
        height: 487px;
        overflow-y: hidden;
        .product-info {
            display: none;
            height: 100%;
            width: 100%;
            color: white;
            padding: 1rem;
            overflow-y: auto;
            img.poster {
                height: 100%;
            }
            div {
                margin-bottom: 1rem;
            }
            .votes {
                color: yellow;
            }
            .language img {
                width: 1.5rem;
                vertical-align: middle;
                margin-left: 0.25rem;
            }
        }
        &:hover .product-info {
            display: block;
            background-color: black;
            position: absolute;
            top: 0;
            left: 0;
        }
    }
</style>