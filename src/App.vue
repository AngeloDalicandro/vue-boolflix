<template>
  <div id="app">

    <HeaderSearchBar @UserSearchText="getUserResearch" />

    <MainContainer :movies="movieSearchResult" :tvSeries="seriesSearchResult"/>

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
      seriesUrl: "https://api.themoviedb.org/3/search/tv?api_key=87180478188b642fd7902412da281198&language=it_IT&query="
    }
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
  }
}
</script>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

</style>
