<template>
  <div id="app">

    <HeaderSearchBar @UserSearchText="getUserResearch" />

    <MainContainer :movies="searchResult"/>

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
      searchResult: [],
      url: "https://api.themoviedb.org/3/search/movie?api_key=87180478188b642fd7902412da281198&language=it&query="
    }
  },
  methods: {
    getUserResearch(research) {
      const userResearch = research.toLowerCase().replace(/ /g, "+");
      
      axios.get(this.url + userResearch).then((result) => {
        this.searchResult = result.data.results
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
