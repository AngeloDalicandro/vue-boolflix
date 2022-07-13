<template>
    <li>

        <img class="poster" v-if="didLoad === true" :src="productImgUrl + series.poster_path" @error="pictureLoadingError" :alt="series.name">
        <img class="poster" v-else :src="productImgUrl + series.backdrop_path"  :alt="series.name">

        <div @mouseleave="resetVisibility()" class="product-info">
            <div class="title"> <b>Titolo: </b> {{ series.name }} </div>
            <div class="original-title"> {{ series.original_name }} </div>
            <div class="language">
                <b>Lingua:</b>
                <img :src="languageImgUrl + enIsNotANation(series.origin_country[0])" :alt="`Original language: ${language[series.original_language]}`">
            </div>
            <div class="votes">
                <b>Voto:</b>
                <span v-for="star, index in fromTenToFive(series.vote_average)" :key="`fullstar-${index}`"><font-awesome-icon icon="fa-solid fa-star"/></span>
                <span v-for="emptyStar, index in ( maxVote - fromTenToFive(series.vote_average))" :key="`emptystar-${index}`"><font-awesome-icon icon="fa-regular fa-star"/></span> 
            </div>
            <div class="overview"> <b>Trama:</b> {{ series.overview }} </div>
            <div class="genre"> <b>Generi:</b> 
                <div v-for="genre, index in series.genre_ids" :key="index"> 
                    <div v-for="genericGenre in seriesGenres.genres" :key="genericGenre.id">
                        <div v-if="genericGenre.id === genre">
                            {{ genericGenre.name }}
                        </div>
                    </div>
                </div>
            </div>
             
            <div class="actors">
                <button @click="getActors(series.id)">Guarda gli attori principali</button>
                <div v-show="actorsVisibility" v-if="actors.length > 0">
                    <div v-for="actor in actors" :key="actor.id">
                        <div>
                            <b>Personaggio:</b> {{ actor.character }} <br>
                            <b>Attore:</b> {{ actor.name }}
                        </div>
                    </div>
                </div>

                <div v-show="actorsVisibility" v-else>
                    Non sono disponibili le informazioni richieste, ci dispiace.
                </div>
            </div>

        </div>

    </li>
</template>

<script>
import languagesList from "../assets/languages.json";
import axios from "axios";
import seriesGenres from "../assets/seriesGenres.json";

export default {
    name: "SeriesCard",
    data() {
        return {
            maxVote: 5,
            language: languagesList,
            languageImgUrl: "https://countryflagsapi.com/svg/",
            productImgUrl: "https://image.tmdb.org/t/p/w342",
            didLoad: true,
            actors: [],
            actorsVisibility: false,
            seriesGenres: seriesGenres
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
        },
        getActors(id) {
            this.actors = [];

            axios.get(`https://api.themoviedb.org/3/movie/${id}/credits?api_key=87180478188b642fd7902412da281198&language=it-IT`).then( (credits) => {
                for( let i = 0; i < 5; i++){
                    this.actors.push(credits.data.cast[i]);
                }
            })
            .catch((err) => {
            console.log(`Error ${err}`)
            });

            this.actorsVisibility = !this.actorsVisibility;
        },
        resetVisibility() {
            this.actorsVisibility = false;
        }
    }
}
</script>

<style lang="scss" scoped>
    @import "../styles/cards-style";
</style>