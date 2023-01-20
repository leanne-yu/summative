<script setup>
import { useStore } from "../store/index.js"
import SiteHeader from "../components/SiteHeader.vue";

const store = useStore();

</script>

<template>
  <SiteHeader />
  <h1 class="cart">THE CART!</h1>
  <div class="cart-movies" v-for="movie in Array.from(store.cart.values())">
    <div class="cart-image">
      <img :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
    </div>
    <div class="cart-info">
      <h1>{{ movie.title }}</h1>
      <p>{{ movie.date }}</p>
      <p>{{ movie.summary }}</p>
    </div>
    <button class="remove-button" @click="store.removeFromCart(movie.id)">Remove</button>
  </div>
</template>

<style scoped>
.cart-movies > .cart-image {
  display: inline-block;
  height: 32vh;
  width: 15vw;
  margin-left: 5%;
  margin-bottom: 5%;
  margin-top: 5%;
  border: none;
  display: flex;
  padding-right: 5%;
  
}

.cart {
  margin: 0%;
  color: rgb(73, 103, 73);
  font-size: 40px;
  font-family: 'Fredoka One';
  margin-top: 1%;
  text-align: center;
  text-decoration: underline;
}

.remove-button {
  position: absolute;
  margin: 0;
  margin-top: 24%;
  margin-left: 24%;
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
  margin: 0%;
  margin-top: 2.5%;
  margin-right: 2.5%;
  color: rgb(18, 78, 18);
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.cart-movies {
  display: flex;
}

</style>