<template>
  <div id="app">

    <HeaderSearchBar @UserSearchText="searchThis" />

    <MainContainer :searchedText="userResearch" />

  </div>
</template>

<script>
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
      userResearch: '',
    }
  },
  methods: {
    searchThis(pippo) {
      this.userResearch = pippo.toLowerCase().replace(/ /g, "-");
    }
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
