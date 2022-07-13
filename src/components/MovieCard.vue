<template>
    
    <li>
        <img class="poster" v-if="didLoad === true" :src="productImgUrl + movie.poster_path" @error="pictureLoadingError" :alt="movie.title">
        <img class="poster" v-else :src="productImgUrl + movie.backdrop_path"  :alt="movie.title">

        <div @mouseleave="resetVisibility()" class="product-info">
            <div class="title"> <b>Titolo:</b> {{ movie.title }} </div>
            <div class="original-title"> <b>Titolo originale:</b> {{ movie.original_title }} </div>
            <div class="language">
                <b>Lingua:</b>
                <img :src="languageImgUrl + enIsNotANation(movie.original_language)" :alt="`Original language: ${language[movie.original_language]}`">
            </div>
            <div class="votes">
                <b>Voto:</b> 
                <span v-for="star, index in fromTenToFive(movie.vote_average)" :key="`fullstar-${index}`"><font-awesome-icon icon="fa-solid fa-star"/></span>
                <span v-for="emptyStar, index in ( maxVote - fromTenToFive(movie.vote_average))" :key="`emptystar-${index}`"><font-awesome-icon icon="fa-regular fa-star"/></span> 
            </div>
            <div class="overview"> <b>Trama:</b> {{ movie.overview }}</div>

            <div class="genre"> <b>Generi:</b> 
                <div v-for="genre, index in movie.genre_ids" :key="index"> 
                    <div v-for="genericGenre in moviesGenres.genres" :key="genericGenre.id">
                        <div v-if="genericGenre.id === genre">
                            {{ genericGenre.name }}
                        </div>
                    </div>
                </div>
            </div>

            <div class="actors">
                <button @click="getActors(movie.id)">Guarda gli attori principali</button>
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
import moviesGenres from "../assets/moviesGenres.json";

export default {
    name: "MainContainer",
    data() {
        return {
            maxVote: 5,
            language: languagesList,
            languageImgUrl: "https://countryflagsapi.com/svg/",
            productImgUrl: "https://image.tmdb.org/t/p/w342",
            didLoad: true,
            actors: [],
            actorsVisibility: false,
            moviesGenres: moviesGenres
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
