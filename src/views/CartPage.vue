<script setup>
import { useStore } from "../store/index.js"
import SiteHeader from "../components/SiteHeader.vue";

const store = useStore();

</script>

<template>
  <h1>My Store</h1>
  <div v-for="movie in Array.from(store.cart.values())">
    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
    <h1>{{ movie.title }}</h1>
    <h1>{{ movie.date }}</h1>
    <button @click="store.removeFromCart(movie.id)">Remove</button>
  </div>
</template>

<style scoped>
img {
  width: 200px;
  aspect-ratio: 2 / 3;
}
h1 {
  color: rgb(19, 83, 19);
  font-size: 35px;
  margin-bottom: 0%;
  font-family: 'Fredoka One';
  margin-top: 1%;
}

</style>