<script setup>
import { ref } from 'vue';
import SiteHeader from '../components/SiteHeader.vue';
import SiteModal from '../components/SiteModal.vue';
import { useStore } from "../store/index.js"

const store = useStore()
const genre = ref()
const showModal = ref(false);
const selectedId = ref(0);

const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};

const closeModal = () => {
  showModal.value = false;
};

const getGenres = async () => {
  await store.getMovies(genre.value);
}
</script>

<template>
  <SiteHeader />
  <h1 class="discover">Discover movies here!</h1>
  <div class="genre-dropdown">
    <RouterLink to="/cart" custom v-slot="{ navigate }">
      <button class="cart-button" @click="navigate" role="link">Cart</button>
    </RouterLink>
    <select v-model="genre" @change="getGenres()">
      <option value="28">Action</option>
      <option value="35">Comedy</option>
      <option value="16">Animation</option>
      <option value="53">Thriller</option>
      <option value="80">Fantasy</option>
    </select>
  </div>
  <br>
  <div class="purchase-container">
    <img v-for="movie in store.movies" :id="movie.id" @click="openModal(movie.id)" class="poster"
      :src="`https://image.tmdb.org/t/p/w500/${movie.poster}`" />
  </div>
  <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
</template>

<style>
.purchase-container {
  display: flex;
  flex-wrap: wrap;
}

.purchase-container>.poster {
  height: 42vh;
  width: 20vw;
  margin-left: 3.5%;
  border: solid;
  border-width: 20%;
  border-radius: 4%;
  border-color: rgb(151, 186, 151);
  margin-top: 50px;
}

.discover {
  text-align: center;
  font-family: 'Fredoka One';
  color: rgb(73, 103, 73);
  margin: 0%;
  margin-bottom: 2.5%;
}

select {
  position: absolute;
  margin-left: 15%;
  font-weight: lighter;
  font-size: 22px;
  text-align: center;
  font-family: 'Sigmar One';
  color: rgb(125, 156, 125);
  background-color: ivory;
  border-radius: 18px;
}

.cart-button {
  position: absolute;
  margin: 0;
  margin-left: 5%;
  background-color: rgb(134, 184, 134);
  padding: 10px 40px;
  height: 40px;
  font-size: larger;
  font-family: 'Fredoka One';
  color: rgb(14, 58, 14);
  border: none;
  border-radius: 18px;
}
</style>