<template>
    <header>
        <div class="logo"></div>

        <div class="search">
            <input @keyup.enter="searchText(searchedText)" v-model="searchedText" type="text">
            <button @click="searchText(searchedText)">Cerca</button>
        </div>
    </header>
</template>

<script>


export default {
    name: "HeaderSearchBar",
    data() {
        return {
            searchedText: '',
        }
    },
    methods: {
        searchText(x) {
            this.$emit('UserSearchText', x)
            console.log(x)
        }
    }
}
</script>

<style lang="scss" scoped>
    header {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 4rem;
        background-color: black ;

        input, button {
            padding: 0.25rem;
        }
    }
</style>
