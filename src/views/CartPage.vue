<script setup>
import { useStore } from "../store/index.js"
import SiteHeader from "../components/SiteHeader.vue";

const store = useStore();

</script>

<template>
  <SiteHeader />
  <h1 class="cart">My Cart</h1>
  <div v-for="movie in Array.from(store.cart.values())">
    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
    <div class="cart-info">
      <h1>{{ movie.title }}</h1>
      <h1>{{ movie.date }}</h1>
      <h1>{{ movie.overview }}</h1>
    </div>
    <button class="remove-button" @click="store.removeFromCart(movie.id)">Remove</button>
  </div>
</template>

<style scoped>
img {
  height: 42vh;
  width: 20vw;
  margin-left: 3.5%;
  margin-bottom: 2%;
  border: solid;
  border-width: 20%;
  border-radius: 4%;
  border-color: rgb(151, 186, 151);
  margin-top: 50px;
  display: flex;
  transform: 50%;
  translate: 50%;
}

.cart {
  margin: 0%;
  color: rgb(73, 103, 73);
  font-size: 35px;
  font-family: 'Fredoka One';
  margin-top: 1%;
  text-align: center;
  text-decoration: underline;
}

.remove-button {
  position: absolute;
  margin: 0;
  margin-left: 3.5%;
  background-color: rgb(134, 184, 134);
  padding: 10px 35px;
  height: 40px;
  font-size: larger;
  font-family: 'Fredoka One';
  color: rgb(14, 58, 14);
  border: none;
  border-radius: 18px;
}

.cart-info {
  text-align: Left;
  font-family: 'Sigmar One';
}
</style>