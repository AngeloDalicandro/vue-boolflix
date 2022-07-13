<template>
    

    <li >
        <img class="poster" v-if="didLoad === true" :src="productImgUrl + movie.poster_path" @error="pictureLoadingError" :alt="movie.title">
        <img class="poster" v-else :src="productImgUrl + movie.backdrop_path"  :alt="movie.title">

        <div class="product-info">
            <div class="title"> <b>Titolo:</b> {{ movie.title }} </div>
            <div class="original-title"> <b>Titolo originale:</b> {{ movie.original_title }} </div>
            <div class="language">
                <b>Lingua:</b>
                <img :src="languageImgUrl + enIsNotANation(movie.original_language)" :alt="`Original language: ${language[movie.original_language]}`">
            </div>
            <div class="votes">
                <b>Voto:</b> 
                <span v-for="star, index in fromTenToFive(movie.vote_average)" :key="index"><font-awesome-icon icon="fa-solid fa-star"/></span>
                <span v-for="emptyStar, index in ( maxVote - fromTenToFive(movie.vote_average))" :key="index"><font-awesome-icon icon="fa-regular fa-star"/></span> 
            </div>
            <div class="overview"> <b>Trama:</b> {{ movie.overview }}</div>
        </div>
    </li>
    
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
            productImgUrl: "https://image.tmdb.org/t/p/w342",
            didLoad: true
        }
    },
    props: {
        movie: Object
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
