<template>
    <li>
        <img class="poster" :src="productImgUrl + movie.poster_path" :alt="movie.title">
                {{ movie.title }}
                {{ movie.original_title }}
                <img :src="languageImgUrl + enIsNotANation(movie.original_language)" :alt="`Original language: ${language[movie.original_language]}`">
                <span v-for="star, index in fromTenToFive(movie.vote_average)" :key="index"><font-awesome-icon icon="fa-solid fa-star"/></span>
                <span v-for="emptyStar, index in ( maxVote - fromTenToFive(movie.vote_average))" :key="index"><font-awesome-icon icon="fa-regular fa-star"/></span> 
    </li>
</template>

<script>
export default {
    name: "ProductCard",   
}
</script>
