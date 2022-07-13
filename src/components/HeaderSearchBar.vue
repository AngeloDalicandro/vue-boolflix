<template>
    <header>
        <h1>BoolFlix</h1>

        <div class="search">
            <input @keyup.enter="searchText(searchedText)" v-model="searchedText" type="text">
            <button @click="searchText(searchedText)">Cerca</button>
        </div>

        <div class="genre-filter">
            <label for="filter-by-genre">Generi:</label>
            <select name="filter-by-genre" id="filter-by-genre">
                <!-- <option v-for="genre in thisSearchGenres" key="index" value=""></option> -->
            </select>
        </div>
    </header>
</template>

<script>
import axios from "axios";

export default {
    name: "HeaderSearchBar",
    data() {
        return {
            searchedText: "",
            genresUrl: "https://api.themoviedb.org/3/genre/movie/list?api_key=87180478188b642fd7902412da281198&language=en-US",
            allGenres : [],
        }
    },
    props: {
        movies: Array,
        tvSeries: Array
    },
    created: {
        getGenres() {
            axios.get(this.genresUrl).then((result) => {
                this.allGenres = result.data;
            })
            .catch((err) => {
                console.log(`Error ${err}`)
            });
        }
    },
    computed: {
        ThisSearchGenres() {
            let thisSearchGenres = ["Tutti"];

            this.movies.forEach((movie) =>
                movie.genre_ids.forEach((genre) => {
                    thisSearchGenres.push(genre);
                })
            );
            this.tvSeries.forEach((series) =>
                series.genre_ids.forEach((genre) => {
                    thisSearchGenres.push(genre);
                })
            );

            return thisSearchGenres;
        }
    },
    methods: {
        searchText(x) {
            this.$emit('UserSearchText', x)
        },
    }
}
</script>

<style lang="scss" scoped>
    header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 4rem;
        background-color: black ;
        margin-bottom: 2rem;

        padding: 0 3rem;

        h1 {
            color: red;
        }

        input {
            width: 15rem;
            margin-right: 1rem;
            padding: 0.25rem
        }

        button {
            padding: 0.25rem 1rem ;
        }
    }
</style>
