<template>
  <div id="app">

    <HeaderSearchBar @UserSearchText="getUserResearch" @changedGenre="setGenre" :movies="movieSearchResult" :tvSeries="seriesSearchResult" />

    <!-- :genreList="filteredGenres" -->

    <MainContainer :movies="movieSearchResult" :tvSeries="seriesSearchResult" :userSelectedGenre="parseInt(userSelectedGenre)" />

  </div>
</template>

<script>
import axios from "axios";

import MainContainer from './components/MainContainer.vue';
import HeaderSearchBar from './components/HeaderSearchBar.vue';

export default {
  name: 'App',
  components: {
    MainContainer,
    HeaderSearchBar,
  },
  data() {
    return {
      movieSearchResult: [],
      seriesSearchResult: [],
      movieUrl: "https://api.themoviedb.org/3/search/movie?api_key=87180478188b642fd7902412da281198&language=it&query=",
      seriesUrl: "https://api.themoviedb.org/3/search/tv?api_key=87180478188b642fd7902412da281198&language=it_IT&query=",
      // movieGenresUrl: "https://api.themoviedb.org/3/genre/movie/list?api_key=87180478188b642fd7902412da281198&language=it-IT",
      // allMovieGenres: [],
      // seriesGenresUrl: "https://api.themoviedb.org/3/genre/tv/list?api_key=87180478188b642fd7902412da281198&language=it-IT",
      // allSeriesGenres: [],
      userSelectedGenre: 420
    }
  },
  mounted() {
    this.getGenres;
  },
  methods: {
    getUserResearch(research) {
      const userResearch = research.toLowerCase().replace(/ /g, "+");

      axios.get(this.movieUrl + userResearch).then((result) => {
        this.movieSearchResult = result.data.results
      })
      .catch((err) => {
        console.log(`Error ${err}`)
      });

      axios.get(this.seriesUrl + userResearch).then((result) => {
        this.seriesSearchResult = result.data.results
      })
      .catch((err) => {
        console.log(`Error ${err}`)
      });
    },
    setGenre(selectedGenre){
      this.userSelectedGenre = selectedGenre;
    },
    // getGenres() {
    //     axios.get(this.movieGenresUrl).then((result) => {
    //         this.allMovieGenres = result.data;
    //     })
    //     .catch((err) => {
    //         console.log(`Error ${err}`)
    //     });

    //     axios.get(this.seriesSearchResult).then((result) => {
    //       this.allSeriesGenres = result.data;
    //     })
    //     .catch((err) => {
    //         console.log(`Error ${err}`)
    //     });
    // },
  }
}
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    background-color: #434343;
  }

  img {
    max-width: 100%;
  }

</style>
