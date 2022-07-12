<template>
    <header>
        <h1>BoolFlix</h1>

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
    }
</style>
