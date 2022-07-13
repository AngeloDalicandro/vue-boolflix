<template>
    <header>
        <h1>BoolFlix</h1>

        <div v-if="thisSearchGenres.length > 1" class="genre-filter">
            <label for="filter-by-genre">Generi:</label>
            <select v-model="selectedGenre" @change="changeGenre(selectedGenre)" name="filter-by-genre" id="filter-by-genre">
                <option v-for="genre in thisSearchGenres" :key="genre.id" :value="genre.id">{{ genre.name }}</option> 
            </select>
        </div>

        <div class="search">
            <input @keyup.enter="searchText(searchedText), setAllGenres()" v-model="searchedText" type="text">
            <button @click="searchText(searchedText), setAllGenres()">Cerca</button>
        </div>
    </header>
</template>

<script>
import moviesGenres from "../assets/moviesGenres.json";
import seriesGenres from "../assets/seriesGenres.json";

export default {
    name: "HeaderSearchBar",
    data() {
        return {
            searchedText: "",
            moviesGenres: moviesGenres.genres,
            seriesGenres: seriesGenres.genres,
            selectedGenre: 420,
        }
    },
    props: {
        movies: Array,
        tvSeries: Array
    },
    computed: {
        thisSearchGenres() {
            let thisSearchGenres = [];

            this.movies.forEach((movie) => {
                movie.genre_ids.forEach((genre) => {
                    if(!thisSearchGenres.includes(genre)) {
                        thisSearchGenres.push(genre);
                    }
                })
            });
            this.tvSeries.forEach((series) =>{
                series.genre_ids.forEach((genre) => {
                    if(!thisSearchGenres.includes(genre)) {
                        thisSearchGenres.push(genre)
                    }
                })
            });

            let filteredGenres = [{name: "Tutti i generi", id: 420}];

            let allGenres = [...this.moviesGenres, this.seriesGenres]

            allGenres.forEach((element) => {
                if(thisSearchGenres.includes(element.id)) {
                    if(!filteredGenres.includes(element)){
                        filteredGenres.push(element)
                    } 
                }
            });

            return filteredGenres; 
        }
    },
    methods: {
        searchText(x) {
            this.$emit('UserSearchText', x)
        },
        changeGenre(x) {
            this.$emit('changedGenre', x)
        },
        setAllGenres() {
            this.selectedGenre = 420;
        }
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

        select {
            padding: 0.25rem 1rem;
        }
    }
</style>
