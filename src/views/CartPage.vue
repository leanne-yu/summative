<script setup>
import { useStore } from "../store/index.js"
import SiteHeader from "../components/SiteHeader.vue";

const store = useStore();
console.log(store.cart);
</script>

<template>
  <SiteHeader />
  <div v-for="movie in Array.from(store.cart.values())">
    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
    <h1>{{movie.title}}</h1>
  </div>
</template>

<style scoped>
img {
  width: 200px;
  aspect-ratio: 2 / 3;
}
</style>